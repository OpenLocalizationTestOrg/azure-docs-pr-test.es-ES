---
title: "Tutorial: integración de Azure Active Directory con el software Cezanne HR | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y el software Cezanne HR."
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
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="560b2-103">Tutorial: Integración de Azure Active Directory con el software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="560b2-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="560b2-104">En este tutorial, obtendrá información sobre cómo integrar Cezanne HR Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="560b2-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="560b2-105">La integración del software Cezanne HR con Azure AD proporciona las siguientes ventajas.</span><span class="sxs-lookup"><span data-stu-id="560b2-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="560b2-106">Puede:</span><span class="sxs-lookup"><span data-stu-id="560b2-106">You can:</span></span>

- <span data-ttu-id="560b2-107">Controlar en Azure AD quién tiene acceso al software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="560b2-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="560b2-108">Permitir que los usuarios inicien sesión automáticamente en el software Cezanne HR con el inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="560b2-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="560b2-109">Administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="560b2-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="560b2-110">Para obtener más información sobre la integración de aplicaciones de software como servicio (SaaS) con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="560b2-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="560b2-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="560b2-111">Prerequisites</span></span>

<span data-ttu-id="560b2-112">Para configurar la integración de Azure AD con el software Cezanne HR, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="560b2-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="560b2-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-113">An Azure AD subscription</span></span>
- <span data-ttu-id="560b2-114">Una suscripción habilitada para el inicio de sesión único en el software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="560b2-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="560b2-115">No se recomienda usar un entorno de producción para probar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="560b2-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="560b2-116">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="560b2-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="560b2-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="560b2-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="560b2-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="560b2-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="560b2-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="560b2-119">Scenario description</span></span>
<span data-ttu-id="560b2-120">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="560b2-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="560b2-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="560b2-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="560b2-122">Adición del software Cezanne HR desde la galería</span><span class="sxs-lookup"><span data-stu-id="560b2-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="560b2-123">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="560b2-124">Adición del software Cezanne HR desde la galería</span><span class="sxs-lookup"><span data-stu-id="560b2-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="560b2-125">Para configurar la integración del software Cezanne HR en Azure AD, agréguelo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="560b2-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="560b2-126">Para agregar el software Cezanne HR desde la galería, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="560b2-127">En el panel izquierdo de **[Azure Portal](https://portal.azure.com)**, seleccione el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="560b2-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Botón "Azure Active Directory"][1]

2. <span data-ttu-id="560b2-129">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="560b2-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Vínculo "Todas las aplicaciones"][2]
    
3. <span data-ttu-id="560b2-131">Para agregar una aplicación nueva, en la parte superior del cuadro de diálogo **Todas las aplicaciones**, seleccione **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="560b2-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    ![Botón “Nueva aplicación”][3]

4. <span data-ttu-id="560b2-133">En el cuadro de búsqueda, escriba **Software Cezanne HR**.</span><span class="sxs-lookup"><span data-stu-id="560b2-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![El cuadro de búsqueda](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="560b2-135">En la lista de resultados, seleccione **Cezanne HR Software** y haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="560b2-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![Lista de resultados](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="560b2-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="560b2-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con el software Cezanne HR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="560b2-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="560b2-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en el software Cezanne HR para el usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="560b2-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="560b2-140">Es decir, debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado del software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="560b2-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="560b2-141">Para establecer la relación de vínculo, asigne el valor **nombre de usuario** del software Cezanne HR como valor de **nombre de usuario** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="560b2-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="560b2-142">Para configurar y probar el inicio de sesión único de Azure AD con el software Cezanne HR, complete los siguientes bloques de creación.</span><span class="sxs-lookup"><span data-stu-id="560b2-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="560b2-143">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="560b2-144">En esta sección, puede habilitar el inicio de sesión único de Azure AD en Azure Portal y configurar el inicio de sesión único en la aplicación del software Cezanne HR de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="560b2-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="560b2-145">En Azure Portal, en la página de integración de la aplicación **Cezanne HR Software**, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="560b2-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Comando "Inicio de sesión único"][4]

2. <span data-ttu-id="560b2-147">Para habilitar el inicio de sesión único, en el cuadro de diálogo **Inicio de sesión único**, seleccione el **Modo** en **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="560b2-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Cuadro "Modo"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="560b2-149">En **Dominio y direcciones URL de Cezanne HR Software**, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![Sección “Dominio y direcciones URL de Cezanne HR Software”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="560b2-151">a.</span><span class="sxs-lookup"><span data-stu-id="560b2-151">a.</span></span> <span data-ttu-id="560b2-152">En el cuadro **URL de inicio de sesión**, escriba una dirección URL que tenga la siguiente sintaxis: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="560b2-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="560b2-153">b.</span><span class="sxs-lookup"><span data-stu-id="560b2-153">b.</span></span> <span data-ttu-id="560b2-154">En el cuadro **URL de respuesta**, escriba una dirección URL que tenga la siguiente sintaxis: `https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="560b2-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="560b2-155">Los valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="560b2-155">The preceding values are not real.</span></span> <span data-ttu-id="560b2-156">Actualícelos con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="560b2-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="560b2-157">Para obtener estos valores, póngase en contacto con el [equipo de soporte al cliente de Cezanne HR Software](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="560b2-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="560b2-158">En **Certificado de firma de SAML**, seleccione **Certificado (Base64)** y, luego, guarde el archivo del certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="560b2-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Sección "Certificado de firma de SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="560b2-160">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-160">Select **Save**.</span></span>

    ![Botón “Guardar”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="560b2-162">En **Configuración de Cezanne HR Software**, seleccione **Configurar Cezanne HR Software** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="560b2-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="560b2-163">Copie el **Identificador de entidad de SAML** y la dirección URL del **Servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="560b2-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![Sección “Configuración de Cezanne HR Software”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="560b2-165">En otra ventana del explorador web, inicie sesión en el inquilino del software Cezanne HR como administrador.</span><span class="sxs-lookup"><span data-stu-id="560b2-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="560b2-166">En el panel izquierdo, seleccione **Configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="560b2-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="560b2-167">Seleccione **Configuración de seguridad** > **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="560b2-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Vínculo “Configuración de inicio de sesión único”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="560b2-169">En el panel **Permitir a los usuarios iniciar sesión mediante el siguiente servicio de inicio de sesión único**, seleccione la casilla **SAML 2.0** y, luego, la opción **Configuración avanzada**.</span><span class="sxs-lookup"><span data-stu-id="560b2-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Opciones de inicio de sesión único](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="560b2-171">Seleccione **Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="560b2-171">Select **Add New**.</span></span>

    ![Botón “Agregar nuevo”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="560b2-173">En **Proveedores de identidades SAML 2.0**, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![Sección “Proveedores de identidades SAML 2.0”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="560b2-175">a.</span><span class="sxs-lookup"><span data-stu-id="560b2-175">a.</span></span> <span data-ttu-id="560b2-176">En el cuadro **Nombre para mostrar**, escriba el nombre de su proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="560b2-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="560b2-177">b.</span><span class="sxs-lookup"><span data-stu-id="560b2-177">b.</span></span> <span data-ttu-id="560b2-178">En el cuadro **Identificador de entidad**, pegue el **Identificador de entidad de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="560b2-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="560b2-179">c.</span><span class="sxs-lookup"><span data-stu-id="560b2-179">c.</span></span> <span data-ttu-id="560b2-180">En el cuadro de lista **Enlace SAML**, seleccione **PUBLICAR**.</span><span class="sxs-lookup"><span data-stu-id="560b2-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="560b2-181">d.</span><span class="sxs-lookup"><span data-stu-id="560b2-181">d.</span></span> <span data-ttu-id="560b2-182">En el cuadro **Punto de conexión de servicio de token de seguridad**, pegue la dirección URL del **Servicio de inicio de sesión único de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="560b2-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="560b2-183">e.</span><span class="sxs-lookup"><span data-stu-id="560b2-183">e.</span></span> <span data-ttu-id="560b2-184">En el cuadro **Nombre de atributo de Id. de usuario**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="560b2-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="560b2-185">f.</span><span class="sxs-lookup"><span data-stu-id="560b2-185">f.</span></span> <span data-ttu-id="560b2-186">Para cargar el certificado descargado de Azure AD, seleccione el botón **CARGAR**.</span><span class="sxs-lookup"><span data-stu-id="560b2-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="560b2-187">g.</span><span class="sxs-lookup"><span data-stu-id="560b2-187">g.</span></span> <span data-ttu-id="560b2-188">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-188">Select **OK**.</span></span> 

12. <span data-ttu-id="560b2-189">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-189">Select **Save**.</span></span>

    ![Botón “Guardar”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="560b2-191">Cuando configure la aplicación, puede leer una versión concisa de las instrucciones anteriores en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="560b2-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="560b2-192">Después de agregar la aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, seleccione la pestaña **Inicio de sesión único**. A continuación, consulte la documentación insertada en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="560b2-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="560b2-193">Para obtener más información sobre la característica de documentación insertada, vea la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="560b2-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="560b2-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-194">Create an Azure AD test user</span></span>
<span data-ttu-id="560b2-195">En esta sección, creará el usuario de prueba Britta Simon en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="560b2-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Usuario de prueba Britta Simon][100]

<span data-ttu-id="560b2-197">Haga lo siguiente para crear un usuario de prueba en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="560b2-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="560b2-198">En el panel izquierdo de **Azure Portal**, seleccione el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="560b2-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Botón "Azure Active Directory"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="560b2-200">Para mostrar una lista de usuarios, seleccione **Usuarios y grupos** > **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="560b2-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Vínculo "Todos los usuarios"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="560b2-202">Se abrirá el cuadro de diálogo **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="560b2-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="560b2-203">Para abrir el cuadro de diálogo **Usuario**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Botón "Agregar"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="560b2-205">En el cuadro de diálogo **Usuario**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-205">In the **User** dialog box, do the following:</span></span>
 
    ![Cuadro de diálogo "Usuario"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="560b2-207">a.</span><span class="sxs-lookup"><span data-stu-id="560b2-207">a.</span></span> <span data-ttu-id="560b2-208">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="560b2-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="560b2-209">b.</span><span class="sxs-lookup"><span data-stu-id="560b2-209">b.</span></span> <span data-ttu-id="560b2-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="560b2-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="560b2-211">c.</span><span class="sxs-lookup"><span data-stu-id="560b2-211">c.</span></span> <span data-ttu-id="560b2-212">Seleccione la casilla **Mostrar contraseña** y, después , anote el valor que se generó en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="560b2-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="560b2-213">d.</span><span class="sxs-lookup"><span data-stu-id="560b2-213">d.</span></span> <span data-ttu-id="560b2-214">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="560b2-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="560b2-215">Creación de un usuario de prueba del software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="560b2-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="560b2-216">Para permitir que los usuarios de Azure AD inicien sesión en el software Cezanne HR, tienen que aprovisionarse en él.</span><span class="sxs-lookup"><span data-stu-id="560b2-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="560b2-217">En el caso del software Cezanne HR, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="560b2-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="560b2-218">Para aprovisionar una cuenta de usuario, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="560b2-219">Inicie sesión en su sitio de la compañía del software Cezanne HR como administrador.</span><span class="sxs-lookup"><span data-stu-id="560b2-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="560b2-220">En el panel izquierdo, seleccione **Configuración del sistema** > **Administrar usuarios** > **Adición de un nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="560b2-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="560b2-221">![Vínculo “Adición de un nuevo usuario”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="560b2-222">En **Detalles de la persona**, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="560b2-223">![Sección "Detalles de la persona"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="560b2-224">a.</span><span class="sxs-lookup"><span data-stu-id="560b2-224">a.</span></span> <span data-ttu-id="560b2-225">Establezca **Usuario interno** en **DESACTIVADO**.</span><span class="sxs-lookup"><span data-stu-id="560b2-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="560b2-226">b.</span><span class="sxs-lookup"><span data-stu-id="560b2-226">b.</span></span> <span data-ttu-id="560b2-227">En el cuadro de texto **Nombre**, escriba el nombre del usuario, por ejemplo, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="560b2-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="560b2-228">c.</span><span class="sxs-lookup"><span data-stu-id="560b2-228">c.</span></span> <span data-ttu-id="560b2-229">En el cuadro de texto **Apellido**, escriba el apellido del usuario, por ejemplo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="560b2-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="560b2-230">d.</span><span class="sxs-lookup"><span data-stu-id="560b2-230">d.</span></span> <span data-ttu-id="560b2-231">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico del usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="560b2-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="560b2-232">En **Información de la cuenta**, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="560b2-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="560b2-233">![Sección “Información de la cuenta”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="560b2-234">a.</span><span class="sxs-lookup"><span data-stu-id="560b2-234">a.</span></span> <span data-ttu-id="560b2-235">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="560b2-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="560b2-236">b.</span><span class="sxs-lookup"><span data-stu-id="560b2-236">b.</span></span> <span data-ttu-id="560b2-237">En el cuadro de texto **Contraseña** , escriba la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="560b2-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="560b2-238">c.</span><span class="sxs-lookup"><span data-stu-id="560b2-238">c.</span></span> <span data-ttu-id="560b2-239">En el cuadro de texto**Rol de seguridad**, seleccione **Profesional de RR.HH**.</span><span class="sxs-lookup"><span data-stu-id="560b2-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="560b2-240">d.</span><span class="sxs-lookup"><span data-stu-id="560b2-240">d.</span></span> <span data-ttu-id="560b2-241">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-241">Select **OK**.</span></span>

5. <span data-ttu-id="560b2-242">En la pestaña **Inicio de sesión único**, en la sección **Identificadores SAML 2.0**, seleccione **Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="560b2-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="560b2-243">![Botón “Agregar nuevo”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="560b2-244">En el cuadro de lista **Proveedor de identidades**, seleccione el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="560b2-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="560b2-245">En el cuadro **Identificador de usuario**, escriba la dirección de correo electrónico de la cuenta de usuario de prueba Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="560b2-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="560b2-246">![Cuadros “Proveedor de identidades” e “Identificador de usuario”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="560b2-247">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-247">Select **Save**.</span></span>

    <span data-ttu-id="560b2-248">![Botón "Guardar"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="560b2-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="560b2-249">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="560b2-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="560b2-250">En esta sección, habilitará al usuario de prueba Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso al software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="560b2-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Acceso de usuario de prueba][200] 

1. <span data-ttu-id="560b2-252">En Azure Portal, abra la vista de aplicaciones y vaya a la vista de directorio.</span><span class="sxs-lookup"><span data-stu-id="560b2-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="560b2-253">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="560b2-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Vínculo "Todas las aplicaciones"][201] 

2. <span data-ttu-id="560b2-255">En la lista de aplicaciones, seleccione **Software Cezanne HR**.</span><span class="sxs-lookup"><span data-stu-id="560b2-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Lista “Aplicaciones”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="560b2-257">En el menú de la izquierda, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="560b2-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="560b2-259">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-259">Select **Add**.</span></span> <span data-ttu-id="560b2-260">Después, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="560b2-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][203]

5. <span data-ttu-id="560b2-262">En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="560b2-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="560b2-263">En el cuadro de diálogo **Usuarios y grupos**, elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="560b2-264">En el cuadro de diálogo **Agregar asignación**, seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="560b2-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="560b2-265">Prueba de SSO</span><span class="sxs-lookup"><span data-stu-id="560b2-265">Test SSO</span></span>

<span data-ttu-id="560b2-266">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="560b2-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="560b2-267">Cuando selecciona el icono del software Cezanne HR en el panel de acceso, inicia sesión automáticamente en la aplicación del software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="560b2-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="560b2-268">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="560b2-268">Next steps</span></span>

* [<span data-ttu-id="560b2-269">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="560b2-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="560b2-270">¿Qué es el acceso a aplicaciones y el SSO con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="560b2-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

