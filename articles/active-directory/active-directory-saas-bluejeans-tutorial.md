---
title: "Tutorial: integración de Azure Active Directory con BlueJeans | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="dda94-103">Tutorial: Integración de Azure Active Directory con BlueJeans</span><span class="sxs-lookup"><span data-stu-id="dda94-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="dda94-104">En este tutorial, obtendrá información sobre cómo integrar BlueJeans con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dda94-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dda94-105">La integración de BlueJeans con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dda94-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dda94-106">En Azure AD puede controlar quién tiene acceso a BlueJeans</span><span class="sxs-lookup"><span data-stu-id="dda94-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="dda94-107">Puede permitir que los usuarios inicien sesión automáticamente en BlueJeans (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dda94-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dda94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dda94-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dda94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dda94-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dda94-110">Prerequisites</span></span>

<span data-ttu-id="dda94-111">Para configurar la integración de Azure AD con BlueJeans, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dda94-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="dda94-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dda94-113">Una suscripción habilitada para el inicio de sesión único en BlueJeans</span><span class="sxs-lookup"><span data-stu-id="dda94-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dda94-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dda94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dda94-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dda94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dda94-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dda94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dda94-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dda94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dda94-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dda94-118">Scenario description</span></span>
<span data-ttu-id="dda94-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dda94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dda94-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="dda94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dda94-121">Incorporación de BlueJeans desde la galería</span><span class="sxs-lookup"><span data-stu-id="dda94-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="dda94-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="dda94-123">Incorporación de BlueJeans desde la galería</span><span class="sxs-lookup"><span data-stu-id="dda94-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="dda94-124">Para configurar la integración de BlueJeans en Azure AD, será preciso que agregue BlueJeans desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="dda94-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dda94-125">**Para agregar BlueJeans desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dda94-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dda94-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dda94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dda94-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dda94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dda94-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dda94-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="dda94-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dda94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="dda94-133">En el cuadro de búsqueda, escriba **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="dda94-133">In the search box, type **BlueJeans**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="dda94-135">En el panel de resultados, seleccione **BlueJeans** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dda94-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dda94-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dda94-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BlueJeans con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dda94-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dda94-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BlueJeans para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dda94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="dda94-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="dda94-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="dda94-141">Para establecer la relación de vínculo, en BlueJeans, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="dda94-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dda94-142">Para configurar y probar el inicio de sesión único de Azure AD con BlueJeans, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dda94-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dda94-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="dda94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dda94-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dda94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dda94-145">**[Creación de un usuario de prueba de BlueJeans](#creating-a-bluejeans-test-user)**: para tener un homólogo de Britta Simon en BlueJeans que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dda94-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dda94-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dda94-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dda94-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="dda94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dda94-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dda94-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="dda94-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="dda94-150">**Para configurar el inicio de sesión único de Azure AD con BlueJeans, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dda94-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="dda94-151">En Azure Portal, en la página de integración de la aplicación **BlueJeans**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dda94-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="dda94-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dda94-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="dda94-155">En la sección **Dominio y direcciones URL de BlueJeans**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dda94-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="dda94-157">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-157">a.</span></span> <span data-ttu-id="dda94-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.BlueJeans.com`.</span><span class="sxs-lookup"><span data-stu-id="dda94-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="dda94-159">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-159">b.</span></span> <span data-ttu-id="dda94-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="dda94-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dda94-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="dda94-161">These values are not real.</span></span> <span data-ttu-id="dda94-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="dda94-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dda94-163">Póngase en contacto con el [equipo de soporte de cliente de BlueJeans](https://support.bluejeans.com/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="dda94-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="dda94-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dda94-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="dda94-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dda94-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dda94-168">En la sección **Configuración de BlueJeans**, haga clic en **Configurar BlueJeans** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dda94-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dda94-169">Copie las **direcciones URL del servicio de inicio de sesión único de SAML, de cambio de contraseña y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="dda94-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="dda94-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la empresa de **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="dda94-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="dda94-172">Vaya a **ADMIN \> Group Settings \> Security**.</span><span class="sxs-lookup"><span data-stu-id="dda94-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="dda94-173">![Administración](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="dda94-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="dda94-174">En la sección **Seguridad** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dda94-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="dda94-175">![Inicio de sesión único de SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Inicio de sesión único de SAML")</span><span class="sxs-lookup"><span data-stu-id="dda94-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="dda94-176">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-176">a.</span></span> <span data-ttu-id="dda94-177">Seleccione **SAML Single Sign On**(Inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="dda94-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="dda94-178">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-178">b.</span></span> <span data-ttu-id="dda94-179">Seleccione **Enable automatic provisioning**(Habilitar aprovisionamiento automático).</span><span class="sxs-lookup"><span data-stu-id="dda94-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="dda94-180">Continúe con los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="dda94-180">Move on with the following steps:</span></span>

    <span data-ttu-id="dda94-181">![Ruta del certificado](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Ruta del certificado")</span><span class="sxs-lookup"><span data-stu-id="dda94-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="dda94-182">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-182">a.</span></span> <span data-ttu-id="dda94-183">Haga clic en **Elegir archivo**y cargue el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="dda94-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="dda94-184">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-184">b.</span></span> <span data-ttu-id="dda94-185">Pegue la **dirección URL del servicio de inicio de sesión único de SAML** en el cuadro de texto **Login URL** (URL de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="dda94-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="dda94-186">c.</span><span class="sxs-lookup"><span data-stu-id="dda94-186">c.</span></span> <span data-ttu-id="dda94-187">Pegue el valor de **Cambiar dirección URL de contraseña** en el cuadro de texto **Dirección URL de cambio de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dda94-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="dda94-188">d.</span><span class="sxs-lookup"><span data-stu-id="dda94-188">d.</span></span> <span data-ttu-id="dda94-189">Pegue la **dirección URL de cierre de sesión** en el cuadro de texto **Logout URL** (URL de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="dda94-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="dda94-190">Continúe con los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="dda94-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="dda94-191">![Guardar cambios](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Guardar cambios")</span><span class="sxs-lookup"><span data-stu-id="dda94-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="dda94-192">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-192">a.</span></span> <span data-ttu-id="dda94-193">En el cuadro de texto **Id. de usuario**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="dda94-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="dda94-194">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-194">b.</span></span> <span data-ttu-id="dda94-195">En el cuadro de texto **Correo electrónico**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="dda94-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="dda94-196">c.</span><span class="sxs-lookup"><span data-stu-id="dda94-196">c.</span></span> <span data-ttu-id="dda94-197">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="dda94-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="dda94-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dda94-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dda94-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="dda94-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dda94-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dda94-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dda94-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="dda94-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dda94-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="dda94-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="dda94-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dda94-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dda94-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dda94-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dda94-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dda94-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dda94-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dda94-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="dda94-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dda94-213">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-213">a.</span></span> <span data-ttu-id="dda94-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dda94-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dda94-215">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-215">b.</span></span> <span data-ttu-id="dda94-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dda94-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dda94-217">c.</span><span class="sxs-lookup"><span data-stu-id="dda94-217">c.</span></span> <span data-ttu-id="dda94-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dda94-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dda94-219">d.</span><span class="sxs-lookup"><span data-stu-id="dda94-219">d.</span></span> <span data-ttu-id="dda94-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dda94-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="dda94-221">Creación de un usuario de prueba de BlueJeans</span><span class="sxs-lookup"><span data-stu-id="dda94-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="dda94-222">Para permitir que los usuarios de Azure AD inicien sesión en BlueJeans, tienen que aprovisionarse en BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="dda94-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="dda94-223">En el caso de BlueJeans, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="dda94-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="dda94-224">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dda94-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="dda94-225">Inicie sesión como administrador en el sitio de la compañía de **BlueJeans** .</span><span class="sxs-lookup"><span data-stu-id="dda94-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="dda94-226">Vaya a **ADMIN \> Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="dda94-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="dda94-227">![Administración](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="dda94-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="dda94-228">La pestaña **Add User** (Agregar usuario) está disponible solo si en la pestaña **Security** (Seguridad), la opción **Enable automatic provisioning** (Habilitar aprovisionamiento automático) está desactivada.</span><span class="sxs-lookup"><span data-stu-id="dda94-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="dda94-229">En la sección **Add User** (Agregar usuario), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dda94-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="dda94-230">![Agregar usuario](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="dda94-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="dda94-231">a.</span><span class="sxs-lookup"><span data-stu-id="dda94-231">a.</span></span> <span data-ttu-id="dda94-232">Escriba los datos de una cuenta de AAD válida que desee aprovisionar en los cuadros de texto correspondientes: **BlueJeans Username** (Nombre de usuario de BlueJeans), **Email address** (Dirección de correo electrónico), **BlueJeans Meeting ID** (Id. de reunión de BlueJeans), **Moderator Passcode** (Código de acceso de moderador), **Full Name** (Nombre completo) y **Company** (Empresa).</span><span class="sxs-lookup"><span data-stu-id="dda94-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="dda94-233">b.</span><span class="sxs-lookup"><span data-stu-id="dda94-233">b.</span></span> <span data-ttu-id="dda94-234">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="dda94-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="dda94-235">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de BlueJeans que proporcione BlueJeans para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="dda94-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dda94-236">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda94-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dda94-237">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="dda94-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="dda94-239">**Para asignar Britta Simon a BlueJeans, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dda94-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="dda94-240">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dda94-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dda94-242">En la lista de aplicaciones, seleccione **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="dda94-242">In the applications list, select **BlueJeans**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="dda94-244">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dda94-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="dda94-246">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dda94-246">Click **Add** button.</span></span> <span data-ttu-id="dda94-247">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dda94-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="dda94-249">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="dda94-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dda94-250">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dda94-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dda94-251">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dda94-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dda94-252">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="dda94-252">Testing single sign-on</span></span>

<span data-ttu-id="dda94-253">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="dda94-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dda94-254">Al hacer clic en el icono de BlueJeans del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="dda94-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="dda94-255">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dda94-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dda94-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dda94-256">Additional resources</span></span>

* [<span data-ttu-id="dda94-257">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dda94-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dda94-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dda94-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

