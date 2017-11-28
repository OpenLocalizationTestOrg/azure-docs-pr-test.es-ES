---
title: "Tutorial: Integración de Azure Active Directory con Merchlogix | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Merchlogix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a1f49bb8-6b17-433d-8f25-9d26fb390e77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: jeedes
ms.openlocfilehash: 44fc8226480cafc130720fbe78aa85ee95caec6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-merchlogix"></a><span data-ttu-id="c1499-103">Tutorial: integración de Azure Active Directory con Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c1499-103">Tutorial: Azure Active Directory integration with Merchlogix</span></span>

<span data-ttu-id="c1499-104">En este tutorial, aprenderá a integrar Merchlogix con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1499-104">In this tutorial, you learn how to integrate Merchlogix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1499-105">Integrar Merchlogix con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c1499-105">Integrating Merchlogix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1499-106">Puede controlar en Azure AD quién tiene acceso a Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-106">You can control in Azure AD who has access to Merchlogix.</span></span>
- <span data-ttu-id="c1499-107">Puede permitir que los usuarios inicien sesión automáticamente en Merchlogix (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1499-107">You can enable your users to automatically get signed-on to Merchlogix (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c1499-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c1499-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c1499-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1499-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1499-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c1499-110">Prerequisites</span></span>

<span data-ttu-id="c1499-111">Para configurar la integración de Azure AD con Merchlogix, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c1499-111">To configure Azure AD integration with Merchlogix, you need the following items:</span></span>

- <span data-ttu-id="c1499-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1499-113">Una suscripción habilitada para el inicio de sesión único en Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c1499-113">A Merchlogix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1499-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c1499-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1499-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c1499-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1499-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c1499-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1499-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1499-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1499-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c1499-118">Scenario description</span></span>
<span data-ttu-id="c1499-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c1499-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1499-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c1499-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1499-121">Adición de Merchlogix desde la galería</span><span class="sxs-lookup"><span data-stu-id="c1499-121">Adding Merchlogix from the gallery</span></span>
2. <span data-ttu-id="c1499-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-merchlogix-from-the-gallery"></a><span data-ttu-id="c1499-123">Adición de Merchlogix desde la galería</span><span class="sxs-lookup"><span data-stu-id="c1499-123">Adding Merchlogix from the gallery</span></span>
<span data-ttu-id="c1499-124">Para configurar la integración de Merchlogix en Azure AD, será preciso que agregue Merchlogix desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c1499-124">To configure the integration of Merchlogix into Azure AD, you need to add Merchlogix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1499-125">**Para agregar Merchlogix desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1499-125">**To add Merchlogix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1499-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1499-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="c1499-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c1499-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1499-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1499-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="c1499-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1499-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="c1499-133">En el cuadro de búsqueda, escriba **Merchlogix**, seleccione **Merchlogix** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1499-133">In the search box, type **Merchlogix**, select **Merchlogix** from result panel then click **Add** button to add the application.</span></span>

    ![Merchlogix en la lista de resultados](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c1499-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c1499-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Merchlogix con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1499-136">In this section, you configure and test Azure AD single sign-on with Merchlogix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1499-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Merchlogix para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1499-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Merchlogix is to a user in Azure AD.</span></span> <span data-ttu-id="c1499-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-138">In other words, a link relationship between an Azure AD user and the related user in Merchlogix needs to be established.</span></span>

<span data-ttu-id="c1499-139">Para establecer la relación de vínculo en Merchlogix, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c1499-139">In Merchlogix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1499-140">Para configurar y probar el inicio de sesión único de Azure AD con Merchlogix, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c1499-140">To configure and test Azure AD single sign-on with Merchlogix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1499-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="c1499-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1499-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1499-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1499-143">**[Creación de un usuario de prueba de Merchlogix](#create-a-merchlogix-test-user)**: para tener un homólogo de Britta Simon en Merchlogix que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1499-143">**[Create a Merchlogix test user](#create-a-merchlogix-test-user)** - to have a counterpart of Britta Simon in Merchlogix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1499-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1499-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1499-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="c1499-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c1499-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c1499-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Merchlogix application.</span></span>

<span data-ttu-id="c1499-148">**Para configurar el inicio de sesión único de Azure AD con Merchlogix, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1499-148">**To configure Azure AD single sign-on with Merchlogix, perform the following steps:**</span></span>

1. <span data-ttu-id="c1499-149">En Azure Portal, en la página de integración de la aplicación **Merchlogix**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c1499-149">In the Azure portal, on the **Merchlogix** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="c1499-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c1499-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_samlbase.png)

3. <span data-ttu-id="c1499-153">En la sección **Dominio y direcciones URL de Merchlogix**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1499-153">On the **Merchlogix Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_url.png)

    <span data-ttu-id="c1499-155">a.</span><span class="sxs-lookup"><span data-stu-id="c1499-155">a.</span></span> <span data-ttu-id="c1499-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<DOMAIN>/login.php?saml=true`.</span><span class="sxs-lookup"><span data-stu-id="c1499-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<DOMAIN>/login.php?saml=true`</span></span>

    <span data-ttu-id="c1499-157">b.</span><span class="sxs-lookup"><span data-stu-id="c1499-157">b.</span></span> <span data-ttu-id="c1499-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span><span class="sxs-lookup"><span data-stu-id="c1499-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c1499-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c1499-159">These values are not real.</span></span> <span data-ttu-id="c1499-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c1499-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c1499-161">Póngase en contacto con el [equipo de soporte técnico de Merchlogix](http://www.merchlogix.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="c1499-161">Contact [Merchlogix support team](http://www.merchlogix.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="c1499-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c1499-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_certificate.png) 

5. <span data-ttu-id="c1499-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c1499-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-merchlogix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1499-166">En la sección **Configuración de Merchlogix**, haga clic en **Configurar Merchlogix** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c1499-166">On the **Merchlogix Configuration** section, click **Configure Merchlogix** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1499-167">Copie los valores de **Dirección URL de cierre de sesión, SAML Entity ID** (Identificador de entidad de SAML) y **SAML Single Sign-On Service URL** (URL de servicio de inicio de sesión único de SAML) de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c1499-167">Copy the **Sign-Out URL, SAML Entity ID,** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_configure.png) 

7. <span data-ttu-id="c1499-169">Para configurar el inicio de sesión único en **Merchlogix**, es preciso enviar los valores descargados de **Certificado (Base64)**, **Dirección URL de cierre de sesión, Identificador de entidad de SAML y Dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Merchlogix](http://www.merchlogix.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="c1499-169">To configure single sign-on on **Merchlogix** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Merchlogix support team](http://www.merchlogix.com/contact/).</span></span> <span data-ttu-id="c1499-170">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="c1499-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c1499-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1499-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1499-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c1499-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1499-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1499-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c1499-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c1499-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1499-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="c1499-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c1499-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1499-178">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1499-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c1499-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c1499-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c1499-182">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c1499-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c1499-184">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1499-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c1499-186">a.</span><span class="sxs-lookup"><span data-stu-id="c1499-186">a.</span></span> <span data-ttu-id="c1499-187">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1499-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1499-188">b.</span><span class="sxs-lookup"><span data-stu-id="c1499-188">b.</span></span> <span data-ttu-id="c1499-189">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1499-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c1499-190">c.</span><span class="sxs-lookup"><span data-stu-id="c1499-190">c.</span></span> <span data-ttu-id="c1499-191">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c1499-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c1499-192">d.</span><span class="sxs-lookup"><span data-stu-id="c1499-192">d.</span></span> <span data-ttu-id="c1499-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c1499-193">Click **Create**.</span></span>
 
### <a name="create-a-merchlogix-test-user"></a><span data-ttu-id="c1499-194">Creación de un usuario de prueba de Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c1499-194">Create a Merchlogix test user</span></span>

<span data-ttu-id="c1499-195">En esta sección, creará un usuario llamado Britta Simon en Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-195">In this section, you create a user called Britta Simon in Merchlogix.</span></span> <span data-ttu-id="c1499-196">Trabaje con el [equipo de soporte técnico de Merchlogix](http://www.merchlogix.com/contact/) para agregar los usuarios a la plataforma de Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-196">Work with [Merchlogix support team](http://www.merchlogix.com/contact/) to add the users in the Merchlogix platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c1499-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1499-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="c1499-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Merchlogix.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="c1499-200">**Para asignar a Britta Simon a Merchlogix, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1499-200">**To assign Britta Simon to Merchlogix, perform the following steps:**</span></span>

1. <span data-ttu-id="c1499-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1499-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c1499-203">En la lista de aplicaciones, seleccione **Merchlogix**.</span><span class="sxs-lookup"><span data-stu-id="c1499-203">In the applications list, select **Merchlogix**.</span></span>

    ![Vínculo a Merchlogix en la lista de aplicaciones](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_app.png)  

3. <span data-ttu-id="c1499-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1499-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="c1499-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c1499-207">Click **Add** button.</span></span> <span data-ttu-id="c1499-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1499-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="c1499-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c1499-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1499-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1499-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1499-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1499-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c1499-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c1499-213">Test single sign-on</span></span>

<span data-ttu-id="c1499-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c1499-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1499-215">Al hacer clic en el icono de Merchlogix en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c1499-215">When you click the Merchlogix tile in the Access Panel, you should get automatically signed-on to your Merchlogix application.</span></span>
<span data-ttu-id="c1499-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1499-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1499-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c1499-217">Additional resources</span></span>

* [<span data-ttu-id="c1499-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1499-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1499-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1499-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_203.png

