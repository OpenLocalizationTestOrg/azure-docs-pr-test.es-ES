---
title: "Tutorial: Integración de Azure Active Directory con Envoy | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Envoy."
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
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="85f5d-103">Tutorial: integración de Azure Active Directory con Envoy</span><span class="sxs-lookup"><span data-stu-id="85f5d-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="85f5d-104">En este tutorial, obtendrá información sobre cómo integrar Envoy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85f5d-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85f5d-105">La integración de Envoy con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="85f5d-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85f5d-106">En Azure AD puede controlar quién tiene acceso a Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="85f5d-107">Puede permitir que los usuarios inicien sesión automáticamente en Envoy (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85f5d-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="85f5d-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="85f5d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="85f5d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85f5d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85f5d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85f5d-110">Prerequisites</span></span>

<span data-ttu-id="85f5d-111">Para configurar la integración de Azure AD con Envoy, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="85f5d-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="85f5d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85f5d-113">Una suscripción habilitada para el inicio de sesión único en Envoy</span><span class="sxs-lookup"><span data-stu-id="85f5d-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85f5d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="85f5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85f5d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="85f5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85f5d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="85f5d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85f5d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85f5d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85f5d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="85f5d-118">Scenario description</span></span>
<span data-ttu-id="85f5d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="85f5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85f5d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="85f5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85f5d-121">Incorporación de Envoy desde la galería</span><span class="sxs-lookup"><span data-stu-id="85f5d-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="85f5d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="85f5d-123">Incorporación de Envoy desde la galería</span><span class="sxs-lookup"><span data-stu-id="85f5d-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="85f5d-124">Para configurar la integración de Envoy en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="85f5d-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85f5d-125">**Para agregar Envoy desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="85f5d-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85f5d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="85f5d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85f5d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="85f5d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="85f5d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="85f5d-133">En el cuadro de búsqueda, escriba **Envoy**, seleccione **Envoy** en el panel de resultados y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85f5d-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy en la lista de resultados](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="85f5d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="85f5d-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Envoy con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85f5d-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85f5d-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Envoy para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85f5d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="85f5d-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="85f5d-139">Para establecer la relación de vínculo, en Envoy, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="85f5d-140">Para configurar y probar el inicio de sesión único de Azure AD con Envoy, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="85f5d-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85f5d-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="85f5d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85f5d-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85f5d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85f5d-143">**[Creación de un usuario de prueba de Envoy](#create-an-envoy-test-user)**: para tener un homólogo de Britta Simon en Envoy que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85f5d-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85f5d-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85f5d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85f5d-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="85f5d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="85f5d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="85f5d-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="85f5d-148">**Para configurar el inicio de sesión único de Azure AD con Envoy, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="85f5d-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="85f5d-149">En Azure Portal, en la página de integración de la aplicación **Envoy**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="85f5d-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="85f5d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="85f5d-153">En la sección **Dominio y direcciones URL de Envoy**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85f5d-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="85f5d-155">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.Envoy.com`.</span><span class="sxs-lookup"><span data-stu-id="85f5d-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="85f5d-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="85f5d-156">This value is not real.</span></span> <span data-ttu-id="85f5d-157">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="85f5d-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="85f5d-158">Póngase en contacto con el [equipo de soporte técnico de Envoy](https://envoy.com/contact/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="85f5d-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="85f5d-159">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="85f5d-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="85f5d-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="85f5d-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85f5d-163">En la sección **Configuración de Envoy**, haga clic en **Configurar Envoy** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="85f5d-164">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="85f5d-166">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Envoy como administrador.</span><span class="sxs-lookup"><span data-stu-id="85f5d-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="85f5d-167">En la barra de herramientas de la parte superior, haga clic en el icono de **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="85f5d-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="85f5d-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="85f5d-169">Haga clic en **Compañía**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-169">Click **Company**.</span></span>

    <span data-ttu-id="85f5d-170">![Compañía](./media/active-directory-saas-envoy-tutorial/ic776783.png "Compañía")</span><span class="sxs-lookup"><span data-stu-id="85f5d-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="85f5d-171">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-171">Click **SAML**.</span></span>

    <span data-ttu-id="85f5d-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="85f5d-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="85f5d-173">En la sección de configuración de **SAML Authentication** (Autenticación de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85f5d-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="85f5d-174">![Autenticación de SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticación de SAML")</span><span class="sxs-lookup"><span data-stu-id="85f5d-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="85f5d-175">La aplicación genera automáticamente el valor del identificador de ubicación de la sede central.</span><span class="sxs-lookup"><span data-stu-id="85f5d-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="85f5d-176">a.</span><span class="sxs-lookup"><span data-stu-id="85f5d-176">a.</span></span> <span data-ttu-id="85f5d-177">En el cuadro de texto **Fingerprint** (Huella digital), pegue el valor de **Huella digital** del certificado que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="85f5d-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="85f5d-178">b.</span><span class="sxs-lookup"><span data-stu-id="85f5d-178">b.</span></span> <span data-ttu-id="85f5d-179">Pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML**, que copió de Azure Portal, en el cuadro de texto **IDENTITY PROVIDER HTTP SAML URL** (Dirección URL de SAML HTTP del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="85f5d-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="85f5d-180">c.</span><span class="sxs-lookup"><span data-stu-id="85f5d-180">c.</span></span> <span data-ttu-id="85f5d-181">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="85f5d-182">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85f5d-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="85f5d-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="85f5d-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="85f5d-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85f5d-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="85f5d-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-185">Create an Azure AD test user</span></span>

<span data-ttu-id="85f5d-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85f5d-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="85f5d-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="85f5d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85f5d-189">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="85f5d-191">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="85f5d-193">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="85f5d-195">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85f5d-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="85f5d-197">a.</span><span class="sxs-lookup"><span data-stu-id="85f5d-197">a.</span></span> <span data-ttu-id="85f5d-198">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85f5d-199">b.</span><span class="sxs-lookup"><span data-stu-id="85f5d-199">b.</span></span> <span data-ttu-id="85f5d-200">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85f5d-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="85f5d-201">c.</span><span class="sxs-lookup"><span data-stu-id="85f5d-201">c.</span></span> <span data-ttu-id="85f5d-202">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="85f5d-203">d.</span><span class="sxs-lookup"><span data-stu-id="85f5d-203">d.</span></span> <span data-ttu-id="85f5d-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="85f5d-205">Creación de un usuario de prueba de Envoy</span><span class="sxs-lookup"><span data-stu-id="85f5d-205">Create an Envoy test user</span></span>

<span data-ttu-id="85f5d-206">No hay elemento de acción para que configure el aprovisionamiento de usuarios en Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="85f5d-207">Cuando un usuario asignado intenta iniciar sesión en Envoy desde el panel de acceso, Envoy comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="85f5d-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="85f5d-208">Si no hay cuentas de usuario disponibles, Envoy crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="85f5d-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="85f5d-209">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85f5d-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="85f5d-210">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="85f5d-212">**Para asignar Britta Simon a Envoy, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="85f5d-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="85f5d-213">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="85f5d-215">En la lista de aplicaciones, seleccione **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-215">In the applications list, select **Envoy**.</span></span>

    ![Vínculo a Envoy en la lista de aplicaciones](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="85f5d-217">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="85f5d-219">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-219">Click **Add** button.</span></span> <span data-ttu-id="85f5d-220">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="85f5d-222">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="85f5d-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85f5d-223">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85f5d-224">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="85f5d-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="85f5d-225">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="85f5d-225">Test single sign-on</span></span>

<span data-ttu-id="85f5d-226">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="85f5d-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85f5d-227">Al hacer clic en el icono de Envoy en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Envoy.</span><span class="sxs-lookup"><span data-stu-id="85f5d-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="85f5d-228">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85f5d-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85f5d-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="85f5d-229">Additional resources</span></span>

* [<span data-ttu-id="85f5d-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85f5d-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85f5d-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85f5d-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

