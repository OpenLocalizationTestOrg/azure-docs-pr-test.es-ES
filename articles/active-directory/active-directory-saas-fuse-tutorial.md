---
title: "Tutorial: integración de Azure Active Directory con Fuse | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Fuse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="fb8d3-103">Tutorial: Integración de Azure Active Directory con Fuse</span><span class="sxs-lookup"><span data-stu-id="fb8d3-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="fb8d3-104">En este tutorial, obtendrá información sobre cómo integrar Fuse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb8d3-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb8d3-105">Integrar Fuse con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fb8d3-106">Puede controlar en Azure AD quién tiene acceso a Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="fb8d3-107">Puede permitir que los usuarios inicien sesión automáticamente en Fuse (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fb8d3-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fb8d3-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb8d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb8d3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb8d3-110">Prerequisites</span></span>

<span data-ttu-id="fb8d3-111">Para configurar la integración de Azure AD con Fuse, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="fb8d3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb8d3-113">Una suscripción habilitada para el inicio de sesión único en Fuse</span><span class="sxs-lookup"><span data-stu-id="fb8d3-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb8d3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb8d3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb8d3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb8d3-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb8d3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb8d3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fb8d3-118">Scenario description</span></span>
<span data-ttu-id="fb8d3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb8d3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb8d3-121">Agregar Fuse desde la galería</span><span class="sxs-lookup"><span data-stu-id="fb8d3-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="fb8d3-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="fb8d3-123">Agregar Fuse desde la galería</span><span class="sxs-lookup"><span data-stu-id="fb8d3-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="fb8d3-124">Para configurar la integración de Fuse en Azure AD, deberá agregar Fuse desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb8d3-125">**Para agregar Fuse desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb8d3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="fb8d3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fb8d3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="fb8d3-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="fb8d3-133">En el cuadro de búsqueda, escriba **Fuse**, seleccione **Fuse** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Fuse en la lista de resultados](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fb8d3-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fb8d3-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Fuse con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb8d3-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb8d3-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Fuse para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="fb8d3-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="fb8d3-139">Para establecer la relación de vínculo, en Fuse, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fb8d3-140">Para configurar y probar el inicio de sesión único de Azure AD con Fuse, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb8d3-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fb8d3-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb8d3-143">**[Creación de un usuario de prueba de Fuse](#create-a-fuse-test-user)** : para tener un homólogo de Britta Simon en Fuse que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb8d3-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb8d3-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fb8d3-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fb8d3-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="fb8d3-148">**Para configurar el inicio de sesión único de Azure AD con Fuse, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="fb8d3-149">En Azure Portal, en la página de integración de la aplicación **Fuse**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="fb8d3-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="fb8d3-153">En la sección **Dominio y direcciones URL de Fuse**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="fb8d3-155">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant name>.fusion-universal.com/`.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb8d3-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-156">This value is not real.</span></span> <span data-ttu-id="fb8d3-157">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fb8d3-158">Póngase en contacto con el [equipo de soporte técnico de Fuse](mailto:support@fusion-universal.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="fb8d3-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="fb8d3-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fb8d3-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb8d3-163">En la sección **Configuración de Fuse**, haga clic en **Configurar Fuse** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fb8d3-164">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="fb8d3-166">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el [equipo de soporte técnico de Fuse](mailto:support@fusion-universal.com) y proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="fb8d3-167">El **archivo de certificado (sin procesar)** descargado</span><span class="sxs-lookup"><span data-stu-id="fb8d3-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="fb8d3-168">La **dirección URL del servicio de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="fb8d3-169">El **identificador de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="fb8d3-170">La **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="fb8d3-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fb8d3-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fb8d3-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fb8d3-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-174">Create an Azure AD test user</span></span>

<span data-ttu-id="fb8d3-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb8d3-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="fb8d3-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb8d3-178">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fb8d3-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fb8d3-182">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fb8d3-184">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb8d3-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fb8d3-186">a.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-186">a.</span></span> <span data-ttu-id="fb8d3-187">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb8d3-188">b.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-188">b.</span></span> <span data-ttu-id="fb8d3-189">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fb8d3-190">c.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-190">c.</span></span> <span data-ttu-id="fb8d3-191">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fb8d3-192">d.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-192">d.</span></span> <span data-ttu-id="fb8d3-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="fb8d3-194">Creación de usuario de prueba de Fuse</span><span class="sxs-lookup"><span data-stu-id="fb8d3-194">Create a Fuse test user</span></span>

<span data-ttu-id="fb8d3-195">En esta sección, creará un usuario llamado Britta Simon en Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="fb8d3-196">Trabaje con el [equipo de soporte técnico de Fuse](mailto:support@fusion-universal.com) para agregar los usuarios a la plataforma de Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fb8d3-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8d3-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="fb8d3-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="fb8d3-200">**Para asignar a Britta Simon a Fuse, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fb8d3-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="fb8d3-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fb8d3-203">En la lista de aplicaciones, seleccione **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-203">In the applications list, select **Fuse**.</span></span>

    ![Vínculo a Fuse en la lista de aplicaciones](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="fb8d3-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="fb8d3-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-207">Click **Add** button.</span></span> <span data-ttu-id="fb8d3-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="fb8d3-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fb8d3-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb8d3-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fb8d3-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="fb8d3-213">Test single sign-on</span></span>

<span data-ttu-id="fb8d3-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fb8d3-215">Al hacer clic en el icono de Fuse en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Fuse.</span><span class="sxs-lookup"><span data-stu-id="fb8d3-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="fb8d3-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb8d3-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb8d3-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fb8d3-217">Additional resources</span></span>

* [<span data-ttu-id="fb8d3-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb8d3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb8d3-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb8d3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

