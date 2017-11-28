---
title: "Tutorial: Integración de Azure Active Directory con Zoho | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="becad-103">Tutorial: Integración de Azure Active Directory con Zoho</span><span class="sxs-lookup"><span data-stu-id="becad-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="becad-104">En este tutorial, obtendrá información sobre cómo integrar Zoho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="becad-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="becad-105">La integración de Zoho con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="becad-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="becad-106">Puede controlar en Azure AD quién tiene acceso a Zoho.</span><span class="sxs-lookup"><span data-stu-id="becad-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="becad-107">Puede permitir que los usuarios inicien sesión automáticamente en Zoho (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becad-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="becad-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="becad-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="becad-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="becad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="becad-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="becad-110">Prerequisites</span></span>

<span data-ttu-id="becad-111">Para configurar la integración de Azure AD con Zoho, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="becad-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="becad-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="becad-113">Una suscripción habilitada para el inicio de sesión único en Zoho</span><span class="sxs-lookup"><span data-stu-id="becad-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="becad-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="becad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="becad-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="becad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="becad-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="becad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="becad-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="becad-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="becad-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="becad-118">Scenario description</span></span>
<span data-ttu-id="becad-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="becad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="becad-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="becad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="becad-121">Incorporación de Zoho desde la galería</span><span class="sxs-lookup"><span data-stu-id="becad-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="becad-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="becad-123">Incorporación de Zoho desde la galería</span><span class="sxs-lookup"><span data-stu-id="becad-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="becad-124">Para configurar la integración de Zoho en Azure AD, deberá agregar Zoho desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="becad-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="becad-125">**Para agregar Zoho desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="becad-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="becad-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="becad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="becad-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="becad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="becad-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="becad-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="becad-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="becad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="becad-133">En el cuadro de búsqueda, escriba **Zoho**, seleccione **Zoho** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="becad-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho en la lista de resultados](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="becad-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="becad-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Zoho con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="becad-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="becad-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Zoho para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becad-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="becad-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Zoho.</span><span class="sxs-lookup"><span data-stu-id="becad-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="becad-139">Para establecer la relación de vínculo, en Zoho, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="becad-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="becad-140">Para configurar y probar el inicio de sesión único de Azure AD con Zoho, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="becad-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="becad-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="becad-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="becad-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becad-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="becad-143">**[Creación de un usuario de prueba de Zoho](#create-a-zoho-test-user)** : para tener un homólogo de Britta Simon en Zoho que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becad-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="becad-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becad-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="becad-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="becad-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="becad-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="becad-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Zoho.</span><span class="sxs-lookup"><span data-stu-id="becad-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="becad-148">**Para configurar el inicio de sesión único de Azure AD con Zoho, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="becad-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="becad-149">En Azure Portal, en la página de integración de la aplicación **Zoho**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="becad-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="becad-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="becad-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="becad-153">En la sección **Dominio y direcciones URL de Zoho**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="becad-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="becad-155">a.</span><span class="sxs-lookup"><span data-stu-id="becad-155">a.</span></span> <span data-ttu-id="becad-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.zohomail.com`.</span><span class="sxs-lookup"><span data-stu-id="becad-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="becad-157">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="becad-157">This value is not real.</span></span> <span data-ttu-id="becad-158">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="becad-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="becad-159">Póngase en contacto con el [equipo de atención al cliente de Zoho](https://www.zoho.com/mail/contact.html) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="becad-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="becad-160">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="becad-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="becad-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="becad-162">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="becad-164">En la sección **Configuración de Zoho**, haga clic en **Configurar Zoho** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="becad-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="becad-165">Copie las **direcciones URL del servicio de inicio de sesión único de SAML, de cambio de contraseña y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="becad-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="becad-167">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zoho Mail como administrador.</span><span class="sxs-lookup"><span data-stu-id="becad-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="becad-168">Vaya al **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="becad-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="becad-169">![Panel de control](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Panel de control")</span><span class="sxs-lookup"><span data-stu-id="becad-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="becad-170">Haga clic en la pestaña **Autenticación SAML** .</span><span class="sxs-lookup"><span data-stu-id="becad-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="becad-171">![Autenticación SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="becad-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="becad-172">En la sección **Detalles de la autenticación SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="becad-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="becad-173">![Detalles de la autenticación SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Detalles de la autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="becad-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="becad-174">a.</span><span class="sxs-lookup"><span data-stu-id="becad-174">a.</span></span> <span data-ttu-id="becad-175">En el cuadro de texto **Login URL** (Dirección URL de inicio de sesión), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="becad-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="becad-176">b.</span><span class="sxs-lookup"><span data-stu-id="becad-176">b.</span></span> <span data-ttu-id="becad-177">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión), pegue la **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="becad-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="becad-178">c.</span><span class="sxs-lookup"><span data-stu-id="becad-178">c.</span></span> <span data-ttu-id="becad-179">En el cuadro de texto **Change Password Link** (Cambiar vínculo de contraseña), pegue el valor de **Cambiar dirección URL de contraseña** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="becad-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="becad-180">d.</span><span class="sxs-lookup"><span data-stu-id="becad-180">d.</span></span> <span data-ttu-id="becad-181">Abra en el Bloc de notas el certificado codificado en Base 64 que descargó de Azure Portal, copie el contenido en el Portapapeles y, luego, péguelo en el cuadro de texto **PublicKey** (Clave pública).</span><span class="sxs-lookup"><span data-stu-id="becad-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="becad-182">e.</span><span class="sxs-lookup"><span data-stu-id="becad-182">e.</span></span> <span data-ttu-id="becad-183">En **Algoritmo**, seleccione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="becad-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="becad-184">f.</span><span class="sxs-lookup"><span data-stu-id="becad-184">f.</span></span> <span data-ttu-id="becad-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="becad-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="becad-186">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="becad-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="becad-187">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="becad-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="becad-188">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="becad-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="becad-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-189">Create an Azure AD test user</span></span>

<span data-ttu-id="becad-190">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="becad-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="becad-192">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="becad-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="becad-193">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="becad-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="becad-195">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="becad-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="becad-197">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="becad-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="becad-199">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="becad-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="becad-201">a.</span><span class="sxs-lookup"><span data-stu-id="becad-201">a.</span></span> <span data-ttu-id="becad-202">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="becad-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="becad-203">b.</span><span class="sxs-lookup"><span data-stu-id="becad-203">b.</span></span> <span data-ttu-id="becad-204">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becad-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="becad-205">c.</span><span class="sxs-lookup"><span data-stu-id="becad-205">c.</span></span> <span data-ttu-id="becad-206">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="becad-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="becad-207">d.</span><span class="sxs-lookup"><span data-stu-id="becad-207">d.</span></span> <span data-ttu-id="becad-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="becad-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="becad-209">Creación de un usuario de prueba de Zoho</span><span class="sxs-lookup"><span data-stu-id="becad-209">Create a Zoho test user</span></span>

<span data-ttu-id="becad-210">Para permitir que los usuarios de Azure AD inicien sesión en Zoho Mail, deben aprovisionarse a Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="becad-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="becad-211">En el caso de Zoho Mail, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="becad-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="becad-212">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Zoho Mail ofrecida por Zoho Mail para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="becad-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="becad-213">Para aprovisionar una cuenta de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="becad-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="becad-214">Inicie sesión en su sitio de la compañía de **Zoho Mail** como administrador.</span><span class="sxs-lookup"><span data-stu-id="becad-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="becad-215">Vaya a **Control Panel \> Mail & Docs** (Panel de control > Correo y documentos) .</span><span class="sxs-lookup"><span data-stu-id="becad-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="becad-216">Vaya a **User Details \> Add User** (Detalles del usuario > Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="becad-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="becad-217">![Agregar usuario](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="becad-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="becad-218">En el cuadro de diálogo **Agregar usuarios** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="becad-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="becad-219">![Agregar usuario](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="becad-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="becad-220">a.</span><span class="sxs-lookup"><span data-stu-id="becad-220">a.</span></span> <span data-ttu-id="becad-221">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="becad-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="becad-222">b.</span><span class="sxs-lookup"><span data-stu-id="becad-222">b.</span></span> <span data-ttu-id="becad-223">En el cuadro de texto **Apellidos**, escriba los apellidos del usuario, en este caso, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="becad-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="becad-224">c.</span><span class="sxs-lookup"><span data-stu-id="becad-224">c.</span></span> <span data-ttu-id="becad-225">En el cuadro de texto **Identificador de correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="becad-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="becad-226">d.</span><span class="sxs-lookup"><span data-stu-id="becad-226">d.</span></span> <span data-ttu-id="becad-227">En el cuadro de texto **Contraseña**, escriba la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="becad-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="becad-228">e.</span><span class="sxs-lookup"><span data-stu-id="becad-228">e.</span></span> <span data-ttu-id="becad-229">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="becad-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="becad-230">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="becad-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="becad-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becad-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="becad-232">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Zoho.</span><span class="sxs-lookup"><span data-stu-id="becad-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="becad-234">**Para asignar el usuario Britta Simon a Zoho, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="becad-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="becad-235">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="becad-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="becad-237">En la lista de aplicaciones, seleccione **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="becad-237">In the applications list, select **Zoho**.</span></span>

    ![Vínculo a Zoho en la lista de aplicaciones](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="becad-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="becad-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="becad-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="becad-241">Click **Add** button.</span></span> <span data-ttu-id="becad-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="becad-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="becad-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="becad-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="becad-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="becad-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="becad-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="becad-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="becad-247">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="becad-247">Test single sign-on</span></span>

<span data-ttu-id="becad-248">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="becad-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="becad-249">Al hacer clic en el icono de Zoho en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Zoho.</span><span class="sxs-lookup"><span data-stu-id="becad-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="becad-250">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="becad-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="becad-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="becad-251">Additional resources</span></span>

* [<span data-ttu-id="becad-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="becad-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="becad-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="becad-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

