---
title: "Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y transferencia de MOVEit - integración de Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="ab65d-103">Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="ab65d-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="ab65d-104">En este tutorial, aprenderá cómo toointegrate MOVEit transferencia: integración de Azure AD con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab65d-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab65d-105">Integración de transferencia de MOVEit - integración de Azure AD con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ab65d-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab65d-106">Puede controlar en Azure AD que tenga acceso tooMOVEit transferencia: integración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="ab65d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMOVEit transferencia: integración de Azure AD (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ab65d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab65d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ab65d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab65d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab65d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ab65d-110">Prerequisites</span></span>

<span data-ttu-id="ab65d-111">tooconfigure integración de Azure AD con la transferencia de MOVEit - integración de Azure AD, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ab65d-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="ab65d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab65d-113">Una suscripción habilitada para el inicio de sesión único en MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="ab65d-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab65d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ab65d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab65d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ab65d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab65d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ab65d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab65d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab65d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab65d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ab65d-118">Scenario description</span></span>
<span data-ttu-id="ab65d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ab65d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab65d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ab65d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab65d-121">Agregar MOVEit transferencia: integración de Azure AD desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ab65d-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="ab65d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="ab65d-123">Agregar MOVEit transferencia: integración de Azure AD desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ab65d-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="ab65d-124">integración de hello tooconfigure de transferencia de MOVEit - integración de Azure AD en Azure AD, deberá tooadd MOVEit transferencia: integración de Azure AD de lista tooyour de hello Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ab65d-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab65d-125">**tooadd MOVEit transferencia: integración de Azure AD desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ab65d-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab65d-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ab65d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="ab65d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab65d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="ab65d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab65d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="ab65d-133">En el cuadro de búsqueda de hello, escriba **MOVEit transferencia: integración de Azure AD**, seleccione **MOVEit transferencia: integración de Azure AD** desde el panel de resultados, a continuación, haga clic en **agregar** hello tooadd de botón aplicación.</span><span class="sxs-lookup"><span data-stu-id="ab65d-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Transferencia de MOVEit - integración de Azure AD en la lista de resultados de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ab65d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ab65d-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con MOVEit Transfer - Azure AD integration con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ab65d-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab65d-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en transferencia de MOVEit - integración de Azure AD es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="ab65d-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en transferencia de MOVEit - integración de Azure AD necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ab65d-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="ab65d-139">En transferencia de MOVEit - integración de Azure AD, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab65d-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab65d-140">tooconfigure y prueba de inicio de sesión único en Azure AD con transferencia MOVEit - integración de Azure AD, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ab65d-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab65d-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ab65d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab65d-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab65d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab65d-143">**[Crear una transferencia de MOVEit - usuario de prueba de integración de Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user) ** - toohave un equivalente de Britta Simon en transferencia de MOVEit - integración de Azure AD que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="ab65d-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab65d-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ab65d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab65d-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ab65d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ab65d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ab65d-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la transferencia de MOVEit - aplicación de integración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="ab65d-148">**inicio de sesión único en tooconfigure Azure AD con la transferencia de MOVEit - integración de Azure AD, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ab65d-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab65d-149">En el portal de Azure, en Hola Hola **MOVEit transferencia: integración de Azure AD** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="ab65d-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ab65d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="ab65d-153">En hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ab65d-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="ab65d-155">a.</span><span class="sxs-lookup"><span data-stu-id="ab65d-155">a.</span></span> <span data-ttu-id="ab65d-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="ab65d-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="ab65d-157">b.</span><span class="sxs-lookup"><span data-stu-id="ab65d-157">b.</span></span> <span data-ttu-id="ab65d-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="ab65d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="ab65d-159">c.</span><span class="sxs-lookup"><span data-stu-id="ab65d-159">c.</span></span> <span data-ttu-id="ab65d-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="ab65d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="ab65d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ab65d-161">These values are not real.</span></span> <span data-ttu-id="ab65d-162">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ab65d-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ab65d-163">Puede hacer referencia a estos valores más tarde en **dirección URL de metadatos del proveedor de servicio** sección o póngase en contacto con [MOVEit transferencia: equipo de soporte técnico de cliente de integración de Azure AD](https://community.ipswitch.com/s/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="ab65d-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="ab65d-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ab65d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="ab65d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ab65d-166">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ab65d-168">Inicie sesión en tooyour MOVEit transferencia inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="ab65d-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="ab65d-169">En el panel de navegación izquierdo de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Sección Configuración en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="ab65d-171">Haga clic en el vínculo **Single Signon** (Inicio de sesión único) que se encuentra en **Security Policies -> User Auth** (Directivas de seguridad -> Autenticación de usuario).</span><span class="sxs-lookup"><span data-stu-id="ab65d-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Directivas de seguridad en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="ab65d-173">Haga clic en el documento de metadatos de Hola de toodownload vínculo de dirección URL de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab65d-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![Dirección URL de metadatos del proveedor de servicios](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="ab65d-175">Comprobar **entityID** coincide con **identificador** en hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="ab65d-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="ab65d-176">Comprobar **AssertionConsumerService** coincide con la dirección URL de ubicación **dirección URL de respuesta** en hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="ab65d-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="ab65d-178">Haga clic en **Agregar proveedor de identidades** botón tooadd un nuevo proveedor de identidad federada.</span><span class="sxs-lookup"><span data-stu-id="ab65d-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Agregación del proveedor de identidades](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="ab65d-180">Haga clic en **Examinar... ** tooselect Hola archivo de metadatos que descargó desde el portal de Azure, a continuación, haga clic en **Agregar proveedor de identidades** hello tooupload el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="ab65d-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Proveedor de identidades de SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="ab65d-182">Seleccione "**Sí**" como **habilitado** en hello **modificar configuración del proveedor de identidad federado... ** página y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="ab65d-184">Hola **editar federado identidad del proveedor de configuración de usuario** página, lleve a cabo Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="ab65d-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Edición de la configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="ab65d-186">a.</span><span class="sxs-lookup"><span data-stu-id="ab65d-186">a.</span></span> <span data-ttu-id="ab65d-187">Seleccione **SAML NameID** en **Login name** (Nombre de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="ab65d-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="ab65d-188">b.</span><span class="sxs-lookup"><span data-stu-id="ab65d-188">b.</span></span> <span data-ttu-id="ab65d-189">Seleccione **otros** como **nombre completo** y Hola **nombre del atributo** cuadro de texto establecer valor de hello: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="ab65d-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="ab65d-190">c.</span><span class="sxs-lookup"><span data-stu-id="ab65d-190">c.</span></span> <span data-ttu-id="ab65d-191">Seleccione **otros** como **correo electrónico** y Hola **nombre del atributo** cuadro de texto establecer valor de hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ab65d-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="ab65d-192">d.</span><span class="sxs-lookup"><span data-stu-id="ab65d-192">d.</span></span> <span data-ttu-id="ab65d-193">Seleccione **Yes** (Sí) en **Auto-create account on signon** (Crear automáticamente cuenta al iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="ab65d-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="ab65d-194">e.</span><span class="sxs-lookup"><span data-stu-id="ab65d-194">e.</span></span> <span data-ttu-id="ab65d-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ab65d-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ab65d-196">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ab65d-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab65d-197">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ab65d-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab65d-198">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab65d-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab65d-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-199">Create an Azure AD test user</span></span>

<span data-ttu-id="ab65d-200">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ab65d-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="ab65d-202">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ab65d-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab65d-203">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="ab65d-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ab65d-205">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ab65d-207">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab65d-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ab65d-209">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ab65d-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ab65d-211">a.</span><span class="sxs-lookup"><span data-stu-id="ab65d-211">a.</span></span> <span data-ttu-id="ab65d-212">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab65d-213">b.</span><span class="sxs-lookup"><span data-stu-id="ab65d-213">b.</span></span> <span data-ttu-id="ab65d-214">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab65d-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ab65d-215">c.</span><span class="sxs-lookup"><span data-stu-id="ab65d-215">c.</span></span> <span data-ttu-id="ab65d-216">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="ab65d-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ab65d-217">d.</span><span class="sxs-lookup"><span data-stu-id="ab65d-217">d.</span></span> <span data-ttu-id="ab65d-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="ab65d-219">Creación de un usuario de prueba de MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="ab65d-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="ab65d-220">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en transferencia de MOVEit - integración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="ab65d-221">MOVEit Transfer - Azure AD integration admite el aprovisionamiento Just-In-Time que ha habilitado.</span><span class="sxs-lookup"><span data-stu-id="ab65d-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="ab65d-222">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="ab65d-222">There is no action item for you in this section.</span></span> <span data-ttu-id="ab65d-223">Se crea un nuevo usuario durante una tooaccess de intento de transferencia de MOVEit - integración de Azure AD si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="ab65d-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ab65d-224">Si necesita un usuario toocreate manualmente, necesita hello toocontact [MOVEit transferencia: equipo de soporte técnico de cliente de integración de Azure AD](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="ab65d-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ab65d-225">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab65d-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ab65d-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMOVEit transferencia: integración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="ab65d-228">**tooassign Britta Simon tooMOVEit transferencia: integración de Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ab65d-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab65d-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ab65d-231">En la lista de aplicaciones de hello, seleccione **MOVEit transferencia: integración de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Transferencia Hello MOVEit - integración de Azure AD vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="ab65d-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="ab65d-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-235">Click **Add** button.</span></span> <span data-ttu-id="ab65d-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="ab65d-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab65d-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab65d-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab65d-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ab65d-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ab65d-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ab65d-241">Test single sign-on</span></span>

<span data-ttu-id="ab65d-242">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ab65d-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab65d-243">Al hacer clic en hello MOVEit transferencia - icono de integración de Azure AD en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión tooyour MOVEit transferencia: aplicación de integración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab65d-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab65d-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ab65d-244">Additional resources</span></span>

* [<span data-ttu-id="ab65d-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab65d-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab65d-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab65d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

