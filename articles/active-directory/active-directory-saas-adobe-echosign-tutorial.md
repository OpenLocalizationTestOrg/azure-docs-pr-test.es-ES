---
title: "Tutorial: Integración de Azure Active Directory con Adobe Sign | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Adobe Sign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="4f38d-103">Tutorial: integración de Azure Active Directory con Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4f38d-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="4f38d-104">En este tutorial, obtendrá información sobre cómo integrar Adobe Sign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f38d-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f38d-105">La integración de Adobe Sign con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4f38d-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f38d-106">En Azure AD se puede controlar quién tiene acceso a Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4f38d-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="4f38d-107">Puede permitir que los usuarios inicien sesión automáticamente en Adobe Sign (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f38d-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f38d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4f38d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f38d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f38d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f38d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f38d-110">Prerequisites</span></span>

<span data-ttu-id="4f38d-111">Para configurar la integración de Azure AD con Adobe Sign, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4f38d-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="4f38d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f38d-113">Una suscripción habilitada para el inicio de sesión único en Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4f38d-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f38d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4f38d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f38d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4f38d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f38d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4f38d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f38d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f38d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f38d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4f38d-118">Scenario description</span></span>
<span data-ttu-id="4f38d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4f38d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f38d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4f38d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f38d-121">Agregar el inicio de sesión de Adobe Sign desde la galería</span><span class="sxs-lookup"><span data-stu-id="4f38d-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="4f38d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="4f38d-123">Agregar el inicio de sesión de Adobe Sign desde la galería</span><span class="sxs-lookup"><span data-stu-id="4f38d-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="4f38d-124">Para configurar la integración de Adobe Sign en Azure AD, será preciso que agregue Adobe Sign desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4f38d-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f38d-125">**Para agregar Adobe Sign desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4f38d-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f38d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f38d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f38d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4f38d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f38d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4f38d-133">En el cuadro de búsqueda, escriba **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-133">In the search box, type **Adobe Sign**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="4f38d-135">En el panel de resultados, seleccione **Adobe Sign** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f38d-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f38d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f38d-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Sign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4f38d-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4f38d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Adobe Sign para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f38d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="4f38d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="4f38d-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="4f38d-141">Para establecer la relación de vínculo, en Adobe Sign, asigne el valor del **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4f38d-142">Para configurar y probar el inicio de sesión único de Azure AD con Adobe Sign, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4f38d-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f38d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="4f38d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f38d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f38d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f38d-145">**[Creación de un usuario de prueba de Adobe Sign](#creating-an-adobe-sign-test-user)**: para tener un homólogo de Britta Simon en Adobe Sign que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f38d-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f38d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f38d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f38d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4f38d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f38d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f38d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="4f38d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="4f38d-150">**Para configurar el inicio de sesión único de Azure AD con Adobe Sign, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4f38d-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="4f38d-151">En Azure Portal, en la página de integración de la aplicación **Adobe Sign**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4f38d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4f38d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="4f38d-155">En la sección **Dominio y direcciones URL de Adobe Sign**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f38d-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="4f38d-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f38d-157">a.</span></span> <span data-ttu-id="4f38d-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.echosign.com/`.</span><span class="sxs-lookup"><span data-stu-id="4f38d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="4f38d-159">b.</span><span class="sxs-lookup"><span data-stu-id="4f38d-159">b.</span></span> <span data-ttu-id="4f38d-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="4f38d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f38d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4f38d-161">These values are not real.</span></span> <span data-ttu-id="4f38d-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4f38d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4f38d-163">Póngase en contacto con el [equipo de soporte al cliente de Adobe Sign](https://helpx.adobe.com/in/contact/support.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="4f38d-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="4f38d-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4f38d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="4f38d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4f38d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f38d-168">En la sección **Configuración de Adobe Sign**, haga clic en **Configurar Adobe Sign** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4f38d-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="4f38d-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Adobe Sign como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f38d-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="4f38d-172">En el menú de la parte superior, haga clic en **Account** (Cuenta) y, después, en el panel de navegación de la izquierda, haga clic en **SAML Settings** (Configuración de SAML) en **Account Settings** (Configuración de la cuenta).</span><span class="sxs-lookup"><span data-stu-id="4f38d-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="4f38d-173">![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="4f38d-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="4f38d-174">En la sección de configuración de SAML, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4f38d-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="4f38d-175">![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="4f38d-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="4f38d-176">a.</span><span class="sxs-lookup"><span data-stu-id="4f38d-176">a.</span></span> <span data-ttu-id="4f38d-177">En **SAML Mode** (Modo de SAML), seleccione **SAML Mandatory** (SAML obligatorio).</span><span class="sxs-lookup"><span data-stu-id="4f38d-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="4f38d-178">b.</span><span class="sxs-lookup"><span data-stu-id="4f38d-178">b.</span></span> <span data-ttu-id="4f38d-179">Seleccione **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**(Permitir a los administradores de cuentas de EchoSign iniciar sesión con sus credenciales de EchoSign).</span><span class="sxs-lookup"><span data-stu-id="4f38d-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="4f38d-180">c.</span><span class="sxs-lookup"><span data-stu-id="4f38d-180">c.</span></span> <span data-ttu-id="4f38d-181">En **User Creation** (Creación de usuario), seleccione **Automatically add users authenticated through SAML** (Agregar automáticamente usuarios autenticados a través de SAML).</span><span class="sxs-lookup"><span data-stu-id="4f38d-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="4f38d-182">Continúe con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4f38d-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="4f38d-183">![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="4f38d-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="4f38d-184">a.</span><span class="sxs-lookup"><span data-stu-id="4f38d-184">a.</span></span> <span data-ttu-id="4f38d-185">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **IdP Entity ID** (Identificador de entidad del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="4f38d-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="4f38d-186">b.</span><span class="sxs-lookup"><span data-stu-id="4f38d-186">b.</span></span> <span data-ttu-id="4f38d-187">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **IdP Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="4f38d-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="4f38d-188">c.</span><span class="sxs-lookup"><span data-stu-id="4f38d-188">c.</span></span> <span data-ttu-id="4f38d-189">Pegue el valor de **Sign-Out URL**  (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **IdP Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="4f38d-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="4f38d-190">d.</span><span class="sxs-lookup"><span data-stu-id="4f38d-190">d.</span></span> <span data-ttu-id="4f38d-191">Abra el archivo de **Certificate(Base64)** (Certificado [Base64]) descargado en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **IdP Certificado** (Certificado del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="4f38d-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="4f38d-192">e.</span><span class="sxs-lookup"><span data-stu-id="4f38d-192">e.</span></span> <span data-ttu-id="4f38d-193">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4f38d-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f38d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4f38d-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4f38d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4f38d-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f38d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f38d-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f38d-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4f38d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4f38d-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4f38d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f38d-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f38d-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f38d-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f38d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f38d-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4f38d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f38d-209">a.</span><span class="sxs-lookup"><span data-stu-id="4f38d-209">a.</span></span> <span data-ttu-id="4f38d-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f38d-211">b.</span><span class="sxs-lookup"><span data-stu-id="4f38d-211">b.</span></span> <span data-ttu-id="4f38d-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f38d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f38d-213">c.</span><span class="sxs-lookup"><span data-stu-id="4f38d-213">c.</span></span> <span data-ttu-id="4f38d-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f38d-215">d.</span><span class="sxs-lookup"><span data-stu-id="4f38d-215">d.</span></span> <span data-ttu-id="4f38d-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="4f38d-217">Creación de un usuario de prueba de Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4f38d-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="4f38d-218">Para permitir que los usuarios de Azure AD inicien sesión en Adobe Sign, tienen que aprovisionarse en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f38d-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="4f38d-219">En el caso de Adobe Sign, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="4f38d-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="4f38d-220">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Adobe Sign que esta le ofrezca para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="4f38d-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="4f38d-221">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="4f38d-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4f38d-222">Inicie sesión en el sitio de la compañía de **Adobe Sign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f38d-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="4f38d-223">En el menú de la parte superior, haga clic en **Account** (Cuenta) y, después, en el panel de navegación de la izquierda, haga clic en **Users & Groups** (Usuarios y grupos) y en **Create a new user** (Crear nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="4f38d-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="4f38d-224">![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="4f38d-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="4f38d-225">En la sección **Create New User** (Crear nuevo usuario), lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4f38d-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="4f38d-226">![Creación de usuarios](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="4f38d-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="4f38d-227">a.</span><span class="sxs-lookup"><span data-stu-id="4f38d-227">a.</span></span> <span data-ttu-id="4f38d-228">Escriba en los campos de texto pertinentes los datos de **Email Address** (Dirección de correo electrónico), **Name** (Nombre) y **Last Name** (Apellidos) de la cuenta de correo válida de AAD que desea aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="4f38d-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="4f38d-229">b.</span><span class="sxs-lookup"><span data-stu-id="4f38d-229">b.</span></span> <span data-ttu-id="4f38d-230">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="4f38d-231">El titular de la cuenta de Azure Active Directory recibe un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="4f38d-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f38d-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f38d-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f38d-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="4f38d-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4f38d-235">**Para asignar a Britta Simon a Adobe Sign, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="4f38d-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="4f38d-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4f38d-238">En la lista de aplicaciones, seleccione **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="4f38d-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4f38d-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-242">Click **Add** button.</span></span> <span data-ttu-id="4f38d-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4f38d-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4f38d-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f38d-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f38d-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4f38d-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f38d-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4f38d-248">Testing single sign-on</span></span>

<span data-ttu-id="4f38d-249">Al hacer clic en el icono de Adobe Sign en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="4f38d-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="4f38d-250">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f38d-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f38d-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4f38d-251">Additional resources</span></span>

* [<span data-ttu-id="4f38d-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f38d-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f38d-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f38d-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

