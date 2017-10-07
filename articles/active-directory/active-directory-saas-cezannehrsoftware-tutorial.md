---
title: "Tutorial: integración de Azure Active Directory con el software Cezanne HR | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el software de recursos humanos Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="44cb0-103">Tutorial: Integración de Azure Active Directory con el software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="44cb0-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="44cb0-104">En este tutorial, aprenderá cómo toointegrate software de recursos humanos Cezanne con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44cb0-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44cb0-105">La integración del software de recursos humanos Cezanne con Azure AD proporciona Hola siguientes ventajas.</span><span class="sxs-lookup"><span data-stu-id="44cb0-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="44cb0-106">Puede:</span><span class="sxs-lookup"><span data-stu-id="44cb0-106">You can:</span></span>

- <span data-ttu-id="44cb0-107">Controlar en Azure AD que tenga acceso tooCezanne el software de recursos humanos.</span><span class="sxs-lookup"><span data-stu-id="44cb0-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="44cb0-108">Habilitar el inicio de sesión de los usuarios tooautomatically en software de recursos humanos tooCezanne con inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44cb0-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="44cb0-109">Administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="44cb0-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="44cb0-110">toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44cb0-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44cb0-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="44cb0-111">Prerequisites</span></span>

<span data-ttu-id="44cb0-112">integración de Azure AD con el software de recursos humanos Cezanne tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="44cb0-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="44cb0-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="44cb0-114">Una suscripción habilitada para el inicio de sesión único en el software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="44cb0-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44cb0-115">pasos de hello tootest en este tutorial, se recomienda que no use un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="44cb0-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="44cb0-116">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="44cb0-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="44cb0-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="44cb0-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44cb0-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44cb0-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44cb0-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="44cb0-119">Scenario description</span></span>
<span data-ttu-id="44cb0-120">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="44cb0-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="44cb0-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="44cb0-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="44cb0-122">Agregar software de recursos humanos Cezanne desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="44cb0-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="44cb0-123">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="44cb0-124">Agregar software de recursos humanos Cezanne de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="44cb0-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="44cb0-125">integración de hello tooconfigure del software de recursos humanos Cezanne en Azure AD, agregar software de recursos humanos Cezanne de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="44cb0-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44cb0-126">tooadd software de recursos humanos Cezanne desde la Galería de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="44cb0-127">Hola  **[portal de Azure](https://portal.azure.com)**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="44cb0-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![botón de "Azure Active Directory" Hello][1]

2. <span data-ttu-id="44cb0-129">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![vínculo de Hello "Todas las aplicaciones"][2]
    
3. <span data-ttu-id="44cb0-131">una nueva aplicación, en parte superior de Hola de hello tooadd **todas las aplicaciones** cuadro de diálogo, seleccione **nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Hola "Nueva aplicación" botón][3]

4. <span data-ttu-id="44cb0-133">En el cuadro de búsqueda de hello, escriba **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![cuadro de búsqueda de Hola](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="44cb0-135">En la lista de resultados de hello, seleccione **Software de recursos humanos Cezanne** y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="44cb0-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![lista de resultados de Hola](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="44cb0-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="44cb0-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con el software Cezanne HR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="44cb0-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44cb0-139">Para toowork SSO, Azure AD necesita usuario de Azure AD toohello de tooknow hello Cezanne HR software equivalente.</span><span class="sxs-lookup"><span data-stu-id="44cb0-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="44cb0-140">En otras palabras, debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado Hola Hola software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="44cb0-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="44cb0-141">relación de vínculo de tooestablish hello, asignar Hola software de recursos humanos Cezanne **nombre de usuario** valor como hello Azure AD **nombre de usuario** valor.</span><span class="sxs-lookup"><span data-stu-id="44cb0-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="44cb0-142">tooconfigure y SSO de Azure AD mediante software de recursos humanos Cezanne, Hola completa después de bloques de creación de la prueba.</span><span class="sxs-lookup"><span data-stu-id="44cb0-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="44cb0-143">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="44cb0-144">En esta sección, puede habilitar SSO de Azure AD en hello portal de Azure y configurar SSO en la aplicación de software de recursos humanos Cezanne haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="44cb0-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="44cb0-145">En el portal de Azure, en Hola Hola **Software de recursos humanos Cezanne** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Hola "Inicio de sesión único" comando][4]

2. <span data-ttu-id="44cb0-147">tooenable SSO, Hola **inicio de sesión único** cuadro de diálogo, seleccione hello **modo** como **sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![cuadro de "Modo de" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="44cb0-149">En **Cezanne HR Software dominio y las direcciones URL**, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Hola "Cezanne HR Software dominio y las direcciones URL" sección](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="44cb0-151">a.</span><span class="sxs-lookup"><span data-stu-id="44cb0-151">a.</span></span> <span data-ttu-id="44cb0-152">Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="44cb0-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="44cb0-153">b.</span><span class="sxs-lookup"><span data-stu-id="44cb0-153">b.</span></span> <span data-ttu-id="44cb0-154">Hola **dirección URL de respuesta** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="44cb0-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="44cb0-155">Hello valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="44cb0-155">hello preceding values are not real.</span></span> <span data-ttu-id="44cb0-156">Actualizarlas con la dirección URL de respuesta real de Hola y dirección URL de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="44cb0-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="44cb0-157">valores de hello tooobtain, Hola contacto [equipo de soporte técnico de recursos humanos Cezanne software cliente](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="44cb0-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="44cb0-158">En **el certificado de firma de SAML**, seleccione **certificado (Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="44cb0-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Hola sección "Certificado de firma de SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="44cb0-160">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-160">Select **Save**.</span></span>

    ![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="44cb0-162">En **configuración de Software de recursos humanos Cezanne**, seleccione **configurar Software de recursos humanos Cezanne** tooopen hello **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="44cb0-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="44cb0-163">Hola copia **Id. de entidad SAML** y **SAML Single Sign-On Service** dirección URL de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="44cb0-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![sección "Configuración de Software de recursos humanos Cezanne" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="44cb0-165">En una ventana del explorador web diferente, inicie sesión en el inquilino de software de recursos humanos Cezanne tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="44cb0-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="44cb0-166">En el panel izquierdo de hello, seleccione **el programa de instalación de sistema**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="44cb0-167">Seleccione **Configuración de seguridad** > **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![vínculo de "Single Sign-On configuración" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="44cb0-169">Hola **permitir que los usuarios toolog en uso Hola después de servicios de inicio de sesión único (SSO)** panel, seleccione hello **SAML 2.0** casilla de verificación y seleccione hello **configuración avanzada** opción.</span><span class="sxs-lookup"><span data-stu-id="44cb0-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Opciones de inicio de sesión único](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="44cb0-171">Seleccione **Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-171">Select **Add New**.</span></span>

    ![botón "Agregar nuevo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="44cb0-173">En **proveedores de identidad SAML 2.0**, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Hola sección "Proveedores de identidad SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="44cb0-175">a.</span><span class="sxs-lookup"><span data-stu-id="44cb0-175">a.</span></span> <span data-ttu-id="44cb0-176">Hola **nombre para mostrar** cuadro, escriba el nombre de Hola de su proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="44cb0-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="44cb0-177">b.</span><span class="sxs-lookup"><span data-stu-id="44cb0-177">b.</span></span> <span data-ttu-id="44cb0-178">Hola **identificador de entidad** cuadro, pegue hello **Id. de entidad SAML** que copió de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="44cb0-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="44cb0-179">c.</span><span class="sxs-lookup"><span data-stu-id="44cb0-179">c.</span></span> <span data-ttu-id="44cb0-180">Hola **enlace SAML** cuadro de lista, seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="44cb0-181">d.</span><span class="sxs-lookup"><span data-stu-id="44cb0-181">d.</span></span> <span data-ttu-id="44cb0-182">Hola **extremo de servicio de Token de seguridad** cuadro, pegue hello **SAML Single Sign-On Service** dirección URL que copió de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="44cb0-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="44cb0-183">e.</span><span class="sxs-lookup"><span data-stu-id="44cb0-183">e.</span></span> <span data-ttu-id="44cb0-184">Hola **nombre de atributo de Id. de usuario** cuadro, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="44cb0-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="44cb0-185">f.</span><span class="sxs-lookup"><span data-stu-id="44cb0-185">f.</span></span> <span data-ttu-id="44cb0-186">Hola tooupload descarga certificado de Azure AD, seleccione hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="44cb0-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="44cb0-187">g.</span><span class="sxs-lookup"><span data-stu-id="44cb0-187">g.</span></span> <span data-ttu-id="44cb0-188">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-188">Select **OK**.</span></span> 

12. <span data-ttu-id="44cb0-189">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-189">Select **Save**.</span></span>

    ![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="44cb0-191">Como configurar la aplicación hello, puede leer una versión concisa de hello precede a instrucciones de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44cb0-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="44cb0-192">Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **inicio de sesión único** ficha. Hola acceso incrusta documentación de hello **configuración** sección.</span><span class="sxs-lookup"><span data-stu-id="44cb0-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="44cb0-193">toolearn más información acerca de la característica de documentación de embedded hello, consulte [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="44cb0-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="44cb0-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-194">Create an Azure AD test user</span></span>
<span data-ttu-id="44cb0-195">En esta sección, creará el usuario de prueba Britta Simon Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="44cb0-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![usuario de prueba de Hello Britta Simon][100]

<span data-ttu-id="44cb0-197">toocreate un usuario de prueba en Azure AD, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="44cb0-198">Hola **portal de Azure**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="44cb0-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![botón de "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44cb0-200">lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos** > **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![vínculo de Hello "Todos los usuarios"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="44cb0-202">Hola **todos los usuarios** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44cb0-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="44cb0-203">Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botón de "Agregar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44cb0-205">Hola **usuario** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![cuadro de diálogo de "Usuario" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44cb0-207">a.</span><span class="sxs-lookup"><span data-stu-id="44cb0-207">a.</span></span> <span data-ttu-id="44cb0-208">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44cb0-209">b.</span><span class="sxs-lookup"><span data-stu-id="44cb0-209">b.</span></span> <span data-ttu-id="44cb0-210">Hola **nombre de usuario** cuadro, escriba el usuario Britta Simon **dirección de correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="44cb0-211">c.</span><span class="sxs-lookup"><span data-stu-id="44cb0-211">c.</span></span> <span data-ttu-id="44cb0-212">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, valor de hello tenga en cuenta que se generó en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="44cb0-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="44cb0-213">d.</span><span class="sxs-lookup"><span data-stu-id="44cb0-213">d.</span></span> <span data-ttu-id="44cb0-214">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="44cb0-215">Creación de un usuario de prueba del software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="44cb0-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="44cb0-216">toosign de usuarios tooenable Azure AD en el software de tooCezanne recursos humanos, se les debe aprovisionar en recursos humanos Cezanne software.</span><span class="sxs-lookup"><span data-stu-id="44cb0-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="44cb0-217">En caso de hello de recursos humanos Cezanne software, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="44cb0-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="44cb0-218">El aprovisionamiento de una cuenta de usuario haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="44cb0-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="44cb0-219">Inicie sesión en tooyour Cezanne HR sitio de la compañía de software como administrador.</span><span class="sxs-lookup"><span data-stu-id="44cb0-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="44cb0-220">En el panel izquierdo de hello, seleccione **el programa de instalación de sistema** > **administrar usuarios** > **Agregar nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="44cb0-221">![vínculo de "Agregar nuevo usuario" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="44cb0-222">En **detalles de la persona**, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="44cb0-223">![sección "Detalles de la persona" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="44cb0-224">a.</span><span class="sxs-lookup"><span data-stu-id="44cb0-224">a.</span></span> <span data-ttu-id="44cb0-225">Establezca **Usuario interno** en **DESACTIVADO**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="44cb0-226">b.</span><span class="sxs-lookup"><span data-stu-id="44cb0-226">b.</span></span> <span data-ttu-id="44cb0-227">Hola **nombre** cuadro, tipo hello nombre del usuario, por ejemplo, **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="44cb0-228">c.</span><span class="sxs-lookup"><span data-stu-id="44cb0-228">c.</span></span> <span data-ttu-id="44cb0-229">Hola **Last Name** cuadro, tipo hello apellidos del usuario, por ejemplo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="44cb0-230">d.</span><span class="sxs-lookup"><span data-stu-id="44cb0-230">d.</span></span> <span data-ttu-id="44cb0-231">Hola **correo electrónico** , escriba la dirección de correo electrónico del usuario de hello, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="44cb0-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="44cb0-232">En **información de la cuenta**, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="44cb0-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="44cb0-233">![sección "Información de cuenta" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="44cb0-234">a.</span><span class="sxs-lookup"><span data-stu-id="44cb0-234">a.</span></span> <span data-ttu-id="44cb0-235">Hola **nombre de usuario** , escriba la dirección de correo electrónico del usuario de hello, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="44cb0-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="44cb0-236">b.</span><span class="sxs-lookup"><span data-stu-id="44cb0-236">b.</span></span> <span data-ttu-id="44cb0-237">Hola **contraseña** , escriba la contraseña del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="44cb0-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="44cb0-238">c.</span><span class="sxs-lookup"><span data-stu-id="44cb0-238">c.</span></span> <span data-ttu-id="44cb0-239">Hola **rol de seguridad** cuadro, seleccione **Professional de recursos humanos**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="44cb0-240">d.</span><span class="sxs-lookup"><span data-stu-id="44cb0-240">d.</span></span> <span data-ttu-id="44cb0-241">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-241">Select **OK**.</span></span>

5. <span data-ttu-id="44cb0-242">En hello **inicio de sesión único** ficha Hola **SAML 2.0 identificadores** sección, seleccione **Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="44cb0-243">![botón "Agregar nuevo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="44cb0-244">Hola **proveedor de identidades** cuadro de lista, seleccione el proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="44cb0-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="44cb0-245">Hola **identificador de usuario** cuadro, escriba la dirección de correo electrónico de hello para la cuenta de prueba usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44cb0-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="44cb0-246">![Hola cuadros "Proveedor de identidades" y "Identificador de usuario"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="44cb0-247">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-247">Select **Save**.</span></span>

    <span data-ttu-id="44cb0-248">![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "usuario")</span><span class="sxs-lookup"><span data-stu-id="44cb0-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="44cb0-249">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44cb0-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="44cb0-250">En esta sección, se habilita el usuario de prueba Britta Simon toouse Azure SSO concediendo acceso tooCezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="44cb0-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Acceso de usuario de prueba][200] 

1. <span data-ttu-id="44cb0-252">Hola portal de Azure, abrir vista de aplicaciones de hello y, a continuación, vaya toohello vista del directorio.</span><span class="sxs-lookup"><span data-stu-id="44cb0-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="44cb0-253">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![vínculo de Hello "Todas las aplicaciones"][201] 

2. <span data-ttu-id="44cb0-255">En la lista de aplicaciones de hello, seleccione **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![lista de "Aplicaciones" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="44cb0-257">En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="44cb0-259">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-259">Select **Add**.</span></span> <span data-ttu-id="44cb0-260">A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][203]

5. <span data-ttu-id="44cb0-262">Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="44cb0-263">Hola **usuarios y grupos** cuadro de diálogo, seleccione **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="44cb0-264">Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="44cb0-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="44cb0-265">Prueba de SSO</span><span class="sxs-lookup"><span data-stu-id="44cb0-265">Test SSO</span></span>

<span data-ttu-id="44cb0-266">En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="44cb0-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="44cb0-267">Cuando se selecciona el icono de software de recursos humanos Cezanne hello en Hola Panel de acceso, iniciar sesión en tooyour automáticamente aplicaciones de software de recursos humanos Cezanne.</span><span class="sxs-lookup"><span data-stu-id="44cb0-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44cb0-268">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44cb0-268">Next steps</span></span>

* [<span data-ttu-id="44cb0-269">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44cb0-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44cb0-270">¿Qué es el acceso a aplicaciones y el SSO con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44cb0-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

