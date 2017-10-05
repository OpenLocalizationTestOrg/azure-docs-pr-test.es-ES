---
title: "Tutorial: Integración de Azure Active Directory con Picturepark | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="659d3-103">Tutorial: Integración de Azure Active Directory con Picturepark</span><span class="sxs-lookup"><span data-stu-id="659d3-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="659d3-104">En este tutorial, obtendrá información sobre cómo integrar Picturepark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="659d3-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="659d3-105">La integración de Picturepark con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="659d3-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="659d3-106">En Azure AD puede controlar quién tiene acceso a Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="659d3-107">Puede permitir que los usuarios inicien sesión automáticamente en Picturepark (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="659d3-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="659d3-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="659d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="659d3-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="659d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="659d3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="659d3-110">Prerequisites</span></span>

<span data-ttu-id="659d3-111">Para configurar la integración de Azure AD con Picturepark, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="659d3-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="659d3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="659d3-113">Una suscripción habilitada para el inicio de sesión único en Picturepark</span><span class="sxs-lookup"><span data-stu-id="659d3-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="659d3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="659d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="659d3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="659d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="659d3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="659d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="659d3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="659d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="659d3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="659d3-118">Scenario description</span></span>
<span data-ttu-id="659d3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="659d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="659d3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="659d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="659d3-121">Incorporación de Picturepark desde la galería</span><span class="sxs-lookup"><span data-stu-id="659d3-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="659d3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="659d3-123">Incorporación de Picturepark desde la galería</span><span class="sxs-lookup"><span data-stu-id="659d3-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="659d3-124">Para configurar la integración de Picturepark en Azure AD, será preciso que agregue Picturepark desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="659d3-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="659d3-125">**Para agregar Picturepark desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="659d3-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="659d3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="659d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="659d3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="659d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="659d3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="659d3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="659d3-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="659d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="659d3-133">En el cuadro de búsqueda, escriba **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="659d3-133">In the search box, type **Picturepark**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="659d3-135">En el panel de resultados, seleccione **Picturepark** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="659d3-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="659d3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="659d3-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Picturepark con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="659d3-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="659d3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Picturepark para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="659d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="659d3-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="659d3-141">Para establecer la relación de vínculo, en Picturepark, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="659d3-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="659d3-142">Para configurar y probar el inicio de sesión único de Azure AD con Picturepark, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="659d3-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="659d3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="659d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="659d3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="659d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="659d3-145">**[Creación de un usuario de prueba de Picturepark](#creating-a-picturepark-test-user)**: el objetivo es tener un homólogo de Britta Simon en Picturepark que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="659d3-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="659d3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="659d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="659d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="659d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="659d3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="659d3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="659d3-150">**Para configurar el inicio de sesión único de Azure AD con Picturepark, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="659d3-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="659d3-151">En Azure Portal, en la página de integración de la aplicación **Picturepark**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="659d3-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="659d3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="659d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="659d3-155">En la sección **Dominio y direcciones URL de Picturepark**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="659d3-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="659d3-157">a.</span><span class="sxs-lookup"><span data-stu-id="659d3-157">a.</span></span> <span data-ttu-id="659d3-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.picturepark.com`.</span><span class="sxs-lookup"><span data-stu-id="659d3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="659d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="659d3-159">b.</span></span> <span data-ttu-id="659d3-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="659d3-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="659d3-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="659d3-161">These values are not real.</span></span> <span data-ttu-id="659d3-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="659d3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="659d3-163">Póngase en contacto con el [equipo de soporte técnico de cliente de Picturepark](https://picturepark.com/about/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="659d3-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="659d3-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="659d3-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="659d3-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="659d3-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="659d3-168">En la sección **Configuración de Picturepark**, haga clic en **Configurar Picturepark** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="659d3-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="659d3-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="659d3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="659d3-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía Picturepark como administrador.</span><span class="sxs-lookup"><span data-stu-id="659d3-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="659d3-172">En la barra de herramientas de la parte superior, haga clic en **Herramientas administrativas** y en **Consola de administración**.</span><span class="sxs-lookup"><span data-stu-id="659d3-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="659d3-173">![Consola de administración](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Consola de administración")</span><span class="sxs-lookup"><span data-stu-id="659d3-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="659d3-174">Haga clic en **Autenticación** y en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="659d3-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="659d3-175">![Autenticación](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="659d3-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="659d3-176">En la sección de **Configuración del proveedor de identidades** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="659d3-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="659d3-177">![Configuración del proveedor de identidades](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuración del proveedor de identidades")</span><span class="sxs-lookup"><span data-stu-id="659d3-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="659d3-178">a.</span><span class="sxs-lookup"><span data-stu-id="659d3-178">a.</span></span> <span data-ttu-id="659d3-179">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="659d3-179">Click **Add**.</span></span>
  
    <span data-ttu-id="659d3-180">b.</span><span class="sxs-lookup"><span data-stu-id="659d3-180">b.</span></span> <span data-ttu-id="659d3-181">Escriba un nombre para su configuración.</span><span class="sxs-lookup"><span data-stu-id="659d3-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="659d3-182">c.</span><span class="sxs-lookup"><span data-stu-id="659d3-182">c.</span></span> <span data-ttu-id="659d3-183">Seleccione **Establecer como predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="659d3-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="659d3-184">d.</span><span class="sxs-lookup"><span data-stu-id="659d3-184">d.</span></span> <span data-ttu-id="659d3-185">En el cuadro de texto **Issuer URI** (URI de emisor), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="659d3-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="659d3-186">e.</span><span class="sxs-lookup"><span data-stu-id="659d3-186">e.</span></span> <span data-ttu-id="659d3-187">En el cuadro de texto **Trusted Issuer Thumb Print** (Huella digital del emisor de confianza), pegue el valor de **huella digital** que copió de la sección **Certificado de firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="659d3-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="659d3-188">Haga clic en **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="659d3-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="659d3-189">Para establecer el atributo **Emailaddress** en el cuadro de texto **Notificación**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="659d3-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="659d3-190">![Configuración](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="659d3-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="659d3-191">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="659d3-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="659d3-192">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="659d3-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="659d3-193">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="659d3-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="659d3-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="659d3-195">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="659d3-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="659d3-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="659d3-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="659d3-198">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="659d3-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="659d3-200">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="659d3-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="659d3-202">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="659d3-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="659d3-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="659d3-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="659d3-206">a.</span><span class="sxs-lookup"><span data-stu-id="659d3-206">a.</span></span> <span data-ttu-id="659d3-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="659d3-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="659d3-208">b.</span><span class="sxs-lookup"><span data-stu-id="659d3-208">b.</span></span> <span data-ttu-id="659d3-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="659d3-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="659d3-210">c.</span><span class="sxs-lookup"><span data-stu-id="659d3-210">c.</span></span> <span data-ttu-id="659d3-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="659d3-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="659d3-212">d.</span><span class="sxs-lookup"><span data-stu-id="659d3-212">d.</span></span> <span data-ttu-id="659d3-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="659d3-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="659d3-214">Creación de un usuario de prueba de Picturepark</span><span class="sxs-lookup"><span data-stu-id="659d3-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="659d3-215">Para permitir que los usuarios de Azure AD inicien sesión en Picturepark, deben aprovisionarse en Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="659d3-216">En el caso de Picturepark, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="659d3-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="659d3-217">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="659d3-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="659d3-218">Inicie sesión en su inquilino de **Picturepark** .</span><span class="sxs-lookup"><span data-stu-id="659d3-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="659d3-219">En la barra de herramientas de la parte superior, haga clic en **Herramientas administrativas** y en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="659d3-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="659d3-220">![Usuarios](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="659d3-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="659d3-221">En la pestaña de **información general de los usuarios**, haga clic **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="659d3-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="659d3-222">![Administración de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="659d3-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="659d3-223">En el cuadro de diálogo **Crear usuario**, siga estos pasos para un usuario válido de Azure Active Directory que desea aprovisionar:</span><span class="sxs-lookup"><span data-stu-id="659d3-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="659d3-224">![Creación de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="659d3-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="659d3-225">a.</span><span class="sxs-lookup"><span data-stu-id="659d3-225">a.</span></span> <span data-ttu-id="659d3-226">En el cuadro de texto **Dirección de correo electrónico**, escriba la **dirección de correo electrónico** del usuario **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="659d3-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="659d3-227">b.</span><span class="sxs-lookup"><span data-stu-id="659d3-227">b.</span></span> <span data-ttu-id="659d3-228">En los cuadros de texto **Contraseña** y **Confirmar contraseña**, escriba la **contraseña** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="659d3-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="659d3-229">c.</span><span class="sxs-lookup"><span data-stu-id="659d3-229">c.</span></span> <span data-ttu-id="659d3-230">En el cuadro de texto **Nombre**, escriba el **nombre** de la usuaria **Britta**.</span><span class="sxs-lookup"><span data-stu-id="659d3-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="659d3-231">d.</span><span class="sxs-lookup"><span data-stu-id="659d3-231">d.</span></span> <span data-ttu-id="659d3-232">En el cuadro de texto **Apellido**, escriba el **apellido** de la usuaria **Simon**.</span><span class="sxs-lookup"><span data-stu-id="659d3-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="659d3-233">e.</span><span class="sxs-lookup"><span data-stu-id="659d3-233">e.</span></span> <span data-ttu-id="659d3-234">En el cuadro de texto **Empresa**, escriba el **nombre de la empresa** del usuario.</span><span class="sxs-lookup"><span data-stu-id="659d3-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="659d3-235">f.</span><span class="sxs-lookup"><span data-stu-id="659d3-235">f.</span></span> <span data-ttu-id="659d3-236">En el cuadro de texto **País**, seleccione el **país** del usuario.</span><span class="sxs-lookup"><span data-stu-id="659d3-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="659d3-237">g.</span><span class="sxs-lookup"><span data-stu-id="659d3-237">g.</span></span> <span data-ttu-id="659d3-238">En el cuadro de texto **ZIP** (Código postal), escriba el **código postal** de la ciudad.</span><span class="sxs-lookup"><span data-stu-id="659d3-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="659d3-239">h.</span><span class="sxs-lookup"><span data-stu-id="659d3-239">h.</span></span> <span data-ttu-id="659d3-240">En el cuadro de texto **Ciudad**, escriba el **nombre de la ciudad** del usuario.</span><span class="sxs-lookup"><span data-stu-id="659d3-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="659d3-241">i.</span><span class="sxs-lookup"><span data-stu-id="659d3-241">i.</span></span> <span data-ttu-id="659d3-242">Seleccione un valor en **Language**(Idioma).</span><span class="sxs-lookup"><span data-stu-id="659d3-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="659d3-243">j.</span><span class="sxs-lookup"><span data-stu-id="659d3-243">j.</span></span> <span data-ttu-id="659d3-244">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="659d3-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="659d3-245">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Picturepark ofrecida por Picturepark para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="659d3-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="659d3-246">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="659d3-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="659d3-247">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="659d3-249">**Para asignar Britta Simon a Picturepark, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="659d3-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="659d3-250">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="659d3-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="659d3-252">En la lista de aplicaciones, seleccione **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="659d3-252">In the applications list, select **Picturepark**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="659d3-254">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="659d3-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="659d3-256">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="659d3-256">Click **Add** button.</span></span> <span data-ttu-id="659d3-257">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="659d3-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="659d3-259">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="659d3-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="659d3-260">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="659d3-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="659d3-261">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="659d3-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="659d3-262">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="659d3-262">Testing single sign-on</span></span>

<span data-ttu-id="659d3-263">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="659d3-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="659d3-264">Al hacer clic en el icono de Picturepark en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Picturepark.</span><span class="sxs-lookup"><span data-stu-id="659d3-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="659d3-265">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="659d3-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="659d3-266">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="659d3-266">Additional resources</span></span>

* [<span data-ttu-id="659d3-267">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="659d3-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="659d3-268">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="659d3-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

