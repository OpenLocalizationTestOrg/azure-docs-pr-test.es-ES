---
title: "Tutorial: integración de Azure Active Directory con DocuSign | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="a8150-103">Tutorial: Integración de Azure Active Directory con DocuSign</span><span class="sxs-lookup"><span data-stu-id="a8150-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="a8150-104">En este tutorial, obtendrá información sobre cómo integrar DocuSign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8150-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8150-105">La integración de DocuSign con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a8150-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8150-106">Puede controlar en Azure AD quién tiene acceso a DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="a8150-107">Puede permitir que los usuarios inicien sesión automáticamente en DocuSign (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8150-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a8150-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8150-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8150-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8150-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a8150-110">Prerequisites</span></span>

<span data-ttu-id="a8150-111">Para configurar la integración de Azure AD con DocuSign, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a8150-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="a8150-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8150-113">Una suscripción habilitada para el inicio de sesión único en DocuSign</span><span class="sxs-lookup"><span data-stu-id="a8150-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8150-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a8150-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8150-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a8150-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8150-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a8150-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8150-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8150-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8150-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a8150-118">Scenario description</span></span>
<span data-ttu-id="a8150-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a8150-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8150-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a8150-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8150-121">Adición de DocuSign desde la galería</span><span class="sxs-lookup"><span data-stu-id="a8150-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="a8150-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="a8150-123">Adición de DocuSign desde la galería</span><span class="sxs-lookup"><span data-stu-id="a8150-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="a8150-124">Para configurar la integración de DocuSign en Azure AD, deberá agregar DocuSign desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a8150-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8150-125">**Para agregar DocuSign desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a8150-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8150-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8150-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8150-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a8150-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8150-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a8150-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a8150-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a8150-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a8150-133">En el cuadro de búsqueda, escriba **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a8150-133">In the search box, type **DocuSign**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="a8150-135">En el panel de resultados, seleccione **DocuSign** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8150-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8150-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8150-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con DocuSign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a8150-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8150-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de DocuSign para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="a8150-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="a8150-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="a8150-142">Para configurar y probar el inicio de sesión único de Azure AD con DocuSign, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a8150-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8150-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a8150-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8150-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8150-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8150-145">**[Creación de un usuario de prueba de DocuSign](#creating-a-docusign-test-user)**: para tener un homólogo de Britta Simon en DocuSign que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8150-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8150-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a8150-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8150-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8150-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="a8150-150">**Para configurar el inicio de sesión único de Azure AD con DocuSign y, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a8150-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="a8150-151">En Azure Portal, en la página de integración de la aplicación **DocuSign**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a8150-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a8150-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a8150-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="a8150-155">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a8150-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="a8150-157">En la sección **Configuración de DocuSign** de Azure Portal, haga clic en **Configure DocuSign** (Configurar DocuSign) para abrir la ventana de configuración de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a8150-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="a8150-158">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a8150-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="a8150-160">En otra ventana del explorador web, inicie sesión en el **Portal de administración de DocuSign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="a8150-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="a8150-161">En el menú de navegación de la izquierda, haga clic en **Domains**(Dominios).</span><span class="sxs-lookup"><span data-stu-id="a8150-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configuración del inicio de sesión único][51]

7. <span data-ttu-id="a8150-163">En el panel derecho, haga clic en **Claim Domain**(Reclamar dominio).</span><span class="sxs-lookup"><span data-stu-id="a8150-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configuración del inicio de sesión único][52]

8. <span data-ttu-id="a8150-165">En el cuadro de diálogo **Claim a domain** (Reclamar un dominio), en el cuadro de texto **Domain Name** (Nombre de dominio), escriba el dominio de la compañía y haga clic en **Claim** (Reclamar).</span><span class="sxs-lookup"><span data-stu-id="a8150-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="a8150-166">Asegúrese de que comprueba el dominio y que su estado es activo.</span><span class="sxs-lookup"><span data-stu-id="a8150-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configuración del inicio de sesión único][53]

9. <span data-ttu-id="a8150-168">En el menú de la izquierda, haga clic en **Identity Providers**</span><span class="sxs-lookup"><span data-stu-id="a8150-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configuración del inicio de sesión único][54]
10. <span data-ttu-id="a8150-170">En el panel derecho, haga clic en **Add Identity Provider**(Agregar proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a8150-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuración del inicio de sesión único][55]

11. <span data-ttu-id="a8150-172">En la página **Identity Provider Settings** (Configuración del proveedor de identidades), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a8150-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configuración del inicio de sesión único][56]

    <span data-ttu-id="a8150-174">a.</span><span class="sxs-lookup"><span data-stu-id="a8150-174">a.</span></span> <span data-ttu-id="a8150-175">En el cuadro de texto **Name** (Nombre), escriba un nombre único para la configuración.</span><span class="sxs-lookup"><span data-stu-id="a8150-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="a8150-176">No utilice espacios.</span><span class="sxs-lookup"><span data-stu-id="a8150-176">Do not use spaces.</span></span>

    <span data-ttu-id="a8150-177">b.</span><span class="sxs-lookup"><span data-stu-id="a8150-177">b.</span></span> <span data-ttu-id="a8150-178">Pegue el **identificador de entidad de SAML** en el cuadro de texto **Emisor de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="a8150-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="a8150-179">c.</span><span class="sxs-lookup"><span data-stu-id="a8150-179">c.</span></span> <span data-ttu-id="a8150-180">Pegue la **dirección URL de servicio de inicio de sesión único de SAML** en el cuadro de texto **Identity Provider Login URL** (URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a8150-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a8150-181">d.</span><span class="sxs-lookup"><span data-stu-id="a8150-181">d.</span></span> <span data-ttu-id="a8150-182">Pegue la **dirección URL de cierre de sesión** en el cuadro de texto **Identity Provider Login URL** (URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a8150-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="a8150-183">e.</span><span class="sxs-lookup"><span data-stu-id="a8150-183">e.</span></span> <span data-ttu-id="a8150-184">Seleccione **Sign AuthN Request**(Firmar solicitud de autenticación).</span><span class="sxs-lookup"><span data-stu-id="a8150-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="a8150-185">f.</span><span class="sxs-lookup"><span data-stu-id="a8150-185">f.</span></span> <span data-ttu-id="a8150-186">En **Send AuthN request by** (Enviar solicitud de autorización por), seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="a8150-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="a8150-187">g.</span><span class="sxs-lookup"><span data-stu-id="a8150-187">g.</span></span> <span data-ttu-id="a8150-188">En **Send logout request by** (Enviar solicitud de cierre de sesión por), seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a8150-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="a8150-189">En la sección **Custom Attribute Mapping** (Asignación de atributos personalizados), elija el campo que desea asignar con la notificación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="a8150-190">En este ejemplo, la notificación **emailaddress** está asociada con el valor de **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="a8150-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="a8150-191">Este es el nombre de notificación predeterminado de Azure AD para la notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="a8150-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="a8150-192">Utilice el **identificador de usuario** adecuado para asignar el usuario de Azure AD a la asignación de usuarios de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="a8150-193">Seleccione el campo apropiado y escriba el valor adecuado según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="a8150-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Configuración del inicio de sesión único][57]

13. <span data-ttu-id="a8150-195">En la sección **Identity Provider Certificate** (Certificado del proveedor de identidades), haga clic en **Add Certificate** (Agregar certificado) y cargue el certificado que ha descargado del Portal del portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8150-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configuración del inicio de sesión único][58]

14. <span data-ttu-id="a8150-197">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="a8150-197">Click **Save**.</span></span>

15. <span data-ttu-id="a8150-198">En la sección **Identity Providers** (Proveedores de identidades), haga clic en **Actions** (Acciones) y luego en **Endpoints** (Puntos de conexión).</span><span class="sxs-lookup"><span data-stu-id="a8150-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuración del inicio de sesión único][59]
 
16. <span data-ttu-id="a8150-200">En el **Portal de administración de DocuSign**, en la sección **View SAML 2.0 Endpoints** (Ver puntos de conexión de SAML 2.0), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a8150-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Configuración del inicio de sesión único][60]
   
    <span data-ttu-id="a8150-202">a.</span><span class="sxs-lookup"><span data-stu-id="a8150-202">a.</span></span> <span data-ttu-id="a8150-203">Copie la **dirección URL del emisor del proveedor de servicios** y, a continuación, pegue en el cuadro de texto **Identificador** en la sección **Dominio y direcciones URL de DocuSign** de Azure Portal siguiendo el siguiente patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="a8150-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="a8150-204">b.</span><span class="sxs-lookup"><span data-stu-id="a8150-204">b.</span></span> <span data-ttu-id="a8150-205">Copie la **dirección URL de inicio del proveedor de servicios** y, a continuación, pegue en el cuadro de texto **URL de inicio de sesión** en la sección **Dominio y direcciones URL de DocuSign** de Azure Portal siguiendo el siguiente patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="a8150-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="a8150-207">c.</span><span class="sxs-lookup"><span data-stu-id="a8150-207">c.</span></span>  <span data-ttu-id="a8150-208">Haga clic en **Close**</span><span class="sxs-lookup"><span data-stu-id="a8150-208">Click **Close**</span></span>
    
17. <span data-ttu-id="a8150-209">En Azure Portal, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a8150-209">On the Azure portal, click **Save**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="a8150-211">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8150-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8150-212">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a8150-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8150-213">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8150-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8150-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8150-215">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a8150-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a8150-217">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a8150-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8150-218">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8150-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8150-220">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a8150-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8150-222">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="a8150-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8150-224">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a8150-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8150-226">a.</span><span class="sxs-lookup"><span data-stu-id="a8150-226">a.</span></span> <span data-ttu-id="a8150-227">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8150-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8150-228">b.</span><span class="sxs-lookup"><span data-stu-id="a8150-228">b.</span></span> <span data-ttu-id="a8150-229">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8150-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8150-230">c.</span><span class="sxs-lookup"><span data-stu-id="a8150-230">c.</span></span> <span data-ttu-id="a8150-231">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a8150-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8150-232">d.</span><span class="sxs-lookup"><span data-stu-id="a8150-232">d.</span></span> <span data-ttu-id="a8150-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a8150-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="a8150-234">Creación de un usuario de prueba de DocuSign</span><span class="sxs-lookup"><span data-stu-id="a8150-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="a8150-235">La aplicación admite **aprovisionamiento de usuarios Just-In-Time** y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8150-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8150-236">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8150-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8150-237">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a8150-239">**Para asignar Britta Simon a DocuSign, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a8150-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="a8150-240">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a8150-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a8150-242">En la lista de aplicaciones, seleccione **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a8150-242">In the applications list, select **DocuSign**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="a8150-244">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a8150-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a8150-246">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a8150-246">Click **Add** button.</span></span> <span data-ttu-id="a8150-247">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a8150-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a8150-249">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8150-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8150-250">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a8150-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8150-251">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a8150-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8150-252">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a8150-252">Testing single sign-on</span></span>

<span data-ttu-id="a8150-253">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a8150-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8150-254">Al hacer clic en el icono de DocuSign en el panel de acceso, debería iniciar sesión automáticamente en su aplicación DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8150-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="a8150-255">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8150-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a8150-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a8150-256">Additional resources</span></span>

* [<span data-ttu-id="a8150-257">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8150-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8150-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8150-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a8150-259">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="a8150-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

