---
title: "Tutorial: Integración de Azure Active Directory con Image Relay | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e Image Relay."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="25f77-103">Tutorial: Integración de Azure Active Directory con Image Relay</span><span class="sxs-lookup"><span data-stu-id="25f77-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="25f77-104">En este tutorial, obtendrá información sobre cómo integrar Image Relay con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25f77-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25f77-105">La integración de Image Relay con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="25f77-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25f77-106">Puede controlar en Azure AD quién tiene acceso a Image Relay</span><span class="sxs-lookup"><span data-stu-id="25f77-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="25f77-107">Puede permitir que los usuarios inicien sesión automáticamente en Image Relay (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25f77-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25f77-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="25f77-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25f77-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25f77-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="25f77-110">Prerequisites</span></span>

<span data-ttu-id="25f77-111">Para configurar la integración de Azure AD con Image Relay, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="25f77-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="25f77-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25f77-113">Una suscripción habilitada para inicio de sesión único en Image Relay</span><span class="sxs-lookup"><span data-stu-id="25f77-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25f77-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="25f77-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25f77-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="25f77-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25f77-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="25f77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25f77-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25f77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25f77-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="25f77-118">Scenario description</span></span>
<span data-ttu-id="25f77-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="25f77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25f77-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="25f77-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25f77-121">Incorporación de Image Relay desde la galería</span><span class="sxs-lookup"><span data-stu-id="25f77-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="25f77-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="25f77-123">Incorporación de Image Relay desde la galería</span><span class="sxs-lookup"><span data-stu-id="25f77-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="25f77-124">Para configurar la integración de Image Relay en Azure AD, es preciso agregar Image Relay desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="25f77-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25f77-125">**Para agregar Image Relay desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="25f77-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25f77-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25f77-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25f77-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="25f77-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25f77-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="25f77-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="25f77-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="25f77-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="25f77-133">En el cuadro de búsqueda, escriba **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="25f77-133">In the search box, type **Image Relay**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="25f77-135">En el panel de resultados, seleccione **Image Relay** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="25f77-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25f77-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25f77-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Image Relay con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="25f77-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25f77-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Image Relay para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25f77-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="25f77-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Image Relay.</span><span class="sxs-lookup"><span data-stu-id="25f77-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="25f77-141">Para establecer la relación de vínculo, en Image Relay, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="25f77-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25f77-142">Para configurar y probar el inicio de sesión único de Azure AD con Image Relay, es necesario completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="25f77-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25f77-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="25f77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="25f77-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25f77-145">**[Creación de un usuario de prueba de Image Relay](#creating-an-image-relay-test-user)**: para tener un homólogo de Britta Simon en Image Relay que esté vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25f77-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="25f77-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25f77-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25f77-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="25f77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25f77-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25f77-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Image Relay.</span><span class="sxs-lookup"><span data-stu-id="25f77-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="25f77-150">**Para configurar el inicio de sesión único de Azure AD con Image Relay, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="25f77-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="25f77-151">En Azure Portal, en la página de integración de la aplicación **Image Relay**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="25f77-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="25f77-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="25f77-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="25f77-155">En la sección **Dominio y direcciones URL de Image Relay**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="25f77-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="25f77-157">a.</span><span class="sxs-lookup"><span data-stu-id="25f77-157">a.</span></span> <span data-ttu-id="25f77-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.imagerelay.com/`.</span><span class="sxs-lookup"><span data-stu-id="25f77-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="25f77-159">b.</span><span class="sxs-lookup"><span data-stu-id="25f77-159">b.</span></span> <span data-ttu-id="25f77-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="25f77-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25f77-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="25f77-161">These values are not real.</span></span> <span data-ttu-id="25f77-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="25f77-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25f77-163">Póngase en contacto con el [equipo de soporte de cliente de Image Relay](http://support.imagerelay.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="25f77-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="25f77-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="25f77-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="25f77-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="25f77-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25f77-168">En la sección **Configuración de Image Relay**, haga clic en **Configurar Image Relay** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="25f77-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25f77-169">Copie los valores de la **dirección URL del servicio de cierre de sesión y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="25f77-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="25f77-171">En otra ventana del explorador, inicie sesión en su sitio de empresa de Image Relay como administrador.</span><span class="sxs-lookup"><span data-stu-id="25f77-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="25f77-172">En la barra de herramientas de la parte superior, haga clic en la carga de trabajo **Users & Permissions** (Usuarios y permisos).</span><span class="sxs-lookup"><span data-stu-id="25f77-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="25f77-174">Haga clic en **Create New Permission**(Crear permiso nuevo).</span><span class="sxs-lookup"><span data-stu-id="25f77-174">Click **Create New Permission**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="25f77-176">En la carga de trabajo **Single Sign On Settings** (Configuración de inicio de sesión único), active la casilla **This Group can only sign-in via Single Sign On** (Este grupo solo puede iniciar sesión mediante inicio de sesión único) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="25f77-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="25f77-178">Vaya a **Account Settings**(Configuración de cuenta).</span><span class="sxs-lookup"><span data-stu-id="25f77-178">Go to **Account Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="25f77-180">Vaya a la carga de trabajo **Single Sign On Settings** (Configuración de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="25f77-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="25f77-182">En el cuadro de diálogo **SAML Settings** (Configuración de SAML), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="25f77-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="25f77-184">a.</span><span class="sxs-lookup"><span data-stu-id="25f77-184">a.</span></span> <span data-ttu-id="25f77-185">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL de inicio de sesión único** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25f77-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="25f77-186">b.</span><span class="sxs-lookup"><span data-stu-id="25f77-186">b.</span></span> <span data-ttu-id="25f77-187">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión), pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25f77-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="25f77-188">c.</span><span class="sxs-lookup"><span data-stu-id="25f77-188">c.</span></span> <span data-ttu-id="25f77-189">En **Name Id Format** (Formato de id. de nombre), seleccione **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="25f77-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="25f77-190">d.</span><span class="sxs-lookup"><span data-stu-id="25f77-190">d.</span></span> <span data-ttu-id="25f77-191">En **Binding Options for Requests from the Service Provider (Image Relay)** [Opciones de enlace para solicitudes del proveedor de servicio (Image Relay)], seleccione **POST Binding** (Enlace POST).</span><span class="sxs-lookup"><span data-stu-id="25f77-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="25f77-192">e.</span><span class="sxs-lookup"><span data-stu-id="25f77-192">e.</span></span> <span data-ttu-id="25f77-193">En **x.509 Certificate** (Certificado x.509), haga clic en **Update Certificate** (Actualizar certificado).</span><span class="sxs-lookup"><span data-stu-id="25f77-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="25f77-195">f.</span><span class="sxs-lookup"><span data-stu-id="25f77-195">f.</span></span> <span data-ttu-id="25f77-196">Abra el certificado descargado en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto x.509 Certificate (Certificado X.509).</span><span class="sxs-lookup"><span data-stu-id="25f77-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="25f77-198">g.</span><span class="sxs-lookup"><span data-stu-id="25f77-198">g.</span></span> <span data-ttu-id="25f77-199">En **Just-In-Time User Provisioning** (Aprovisionamiento de usuarios Just-In-Time), active la casilla **Enable Just-In-Time User Provisioning** (Habilitar aprovisionamiento de usuarios Just-In-Time).</span><span class="sxs-lookup"><span data-stu-id="25f77-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="25f77-201">h.</span><span class="sxs-lookup"><span data-stu-id="25f77-201">h.</span></span> <span data-ttu-id="25f77-202">Seleccione el grupo de permisos, por ejemplo, **SSO Basic**(SSO básico), que puede iniciar sesión solo mediante inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="25f77-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="25f77-204">i.</span><span class="sxs-lookup"><span data-stu-id="25f77-204">i.</span></span> <span data-ttu-id="25f77-205">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="25f77-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="25f77-206">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="25f77-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25f77-207">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="25f77-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25f77-208">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25f77-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25f77-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="25f77-210">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="25f77-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="25f77-212">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="25f77-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25f77-213">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25f77-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25f77-215">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="25f77-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25f77-217">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="25f77-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25f77-219">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="25f77-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25f77-221">a.</span><span class="sxs-lookup"><span data-stu-id="25f77-221">a.</span></span> <span data-ttu-id="25f77-222">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25f77-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25f77-223">b.</span><span class="sxs-lookup"><span data-stu-id="25f77-223">b.</span></span> <span data-ttu-id="25f77-224">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f77-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25f77-225">c.</span><span class="sxs-lookup"><span data-stu-id="25f77-225">c.</span></span> <span data-ttu-id="25f77-226">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="25f77-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="25f77-227">d.</span><span class="sxs-lookup"><span data-stu-id="25f77-227">d.</span></span> <span data-ttu-id="25f77-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="25f77-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="25f77-229">Creación de un usuario de prueba de Image Relay</span><span class="sxs-lookup"><span data-stu-id="25f77-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="25f77-230">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Image Relay.</span><span class="sxs-lookup"><span data-stu-id="25f77-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="25f77-231">**Para crear un usuario llamado Britta Simon en Image Relay, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="25f77-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="25f77-232">Inicie sesión en su sitio de empresa de Image Relay como administrador.</span><span class="sxs-lookup"><span data-stu-id="25f77-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="25f77-233">Vaya a **Users & Permissions** (Usuarios y permisos) y seleccione **Create SSO User** (Crear usuario de SSO).</span><span class="sxs-lookup"><span data-stu-id="25f77-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="25f77-235">Escriba los valores de los campos **Email** (Correo electrónico), **First Name** (Nombre), **Last Name** (Apellidos) y **Company** (Empresa) del usuario que desea aprovisionar y seleccione el grupo de permisos, por ejemplo, SSO Basic (SSO básico), que es el grupo que solo puede iniciar sesión mediante inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="25f77-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="25f77-237">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="25f77-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="25f77-238">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f77-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="25f77-239">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Image Relay.</span><span class="sxs-lookup"><span data-stu-id="25f77-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="25f77-241">**Para asignar Britta Simon a Image Relay, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="25f77-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="25f77-242">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="25f77-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="25f77-244">En la lista de aplicaciones, seleccione **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="25f77-244">In the applications list, select **Image Relay**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="25f77-246">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="25f77-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="25f77-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="25f77-248">Click **Add** button.</span></span> <span data-ttu-id="25f77-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="25f77-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="25f77-251">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="25f77-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="25f77-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="25f77-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25f77-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="25f77-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25f77-254">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="25f77-254">Testing single sign-on</span></span>

<span data-ttu-id="25f77-255">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="25f77-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="25f77-256">Al hacer clic en el icono de Image Relay en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Image Relay.</span><span class="sxs-lookup"><span data-stu-id="25f77-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="25f77-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="25f77-257">Additional resources</span></span>

* [<span data-ttu-id="25f77-258">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25f77-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25f77-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25f77-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

