---
title: "Tutorial: integración de Azure Active Directory con TigerText Secure Messenger | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="aa69d-103">Tutorial: integración de Azure Active Directory con TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="aa69d-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="aa69d-104">En este tutorial, obtendrá información sobre cómo integrar TigerText Secure Messenger con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa69d-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa69d-105">La integración de TigerText Secure Messenger con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aa69d-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa69d-106">Puede controlar en Azure AD quién tiene acceso a TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="aa69d-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="aa69d-107">Puede permitir que los usuarios inicien sesión automáticamente en TigerText Secure Messenger (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa69d-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa69d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aa69d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa69d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa69d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa69d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa69d-110">Prerequisites</span></span>

<span data-ttu-id="aa69d-111">Para configurar la integración de Azure AD con TigerText Secure Messenger, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aa69d-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="aa69d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa69d-113">Una suscripción habilitada para el inicio de sesión único en TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="aa69d-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa69d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aa69d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa69d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aa69d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa69d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa69d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa69d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa69d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa69d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aa69d-118">Scenario description</span></span>
<span data-ttu-id="aa69d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aa69d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa69d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="aa69d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa69d-121">Agregar TigerText Secure Messenger desde la galería</span><span class="sxs-lookup"><span data-stu-id="aa69d-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="aa69d-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="aa69d-123">Agregar TigerText Secure Messenger desde la galería</span><span class="sxs-lookup"><span data-stu-id="aa69d-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="aa69d-124">Para configurar la integración de TigerText Secure Messenger en Azure AD, será preciso que agregue TigerText Secure Messenger desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="aa69d-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa69d-125">**Para agregar TigerText Secure Messenger desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="aa69d-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa69d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa69d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa69d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="aa69d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa69d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="aa69d-133">En el cuadro de búsqueda, escriba **TigerText Secure Messenger**, seleccione **TigerText Secure Messenger** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa69d-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Incorporación de la aplicación desde la galería](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="aa69d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="aa69d-136">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con TigerText Secure Messenger con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa69d-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa69d-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TigerText Secure Messenger para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa69d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="aa69d-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="aa69d-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="aa69d-139">Para establecer la relación de vínculo, en TigerText Secure Messenger, asigne el valor del **nombre de usuario** de Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aa69d-140">Para configurar y probar el inicio de sesión único de Azure AD con TigerText Secure Messenger, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aa69d-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa69d-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="aa69d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa69d-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa69d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa69d-143">**[Creación de un usuario de prueba de TigerText](#create-a-tigertext-secure-messenger-test-user)**: para tener un homólogo de Britta Simon en TigerText Secure Messenger que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa69d-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa69d-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa69d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa69d-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aa69d-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="aa69d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="aa69d-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="aa69d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="aa69d-148">**Para configurar el inicio de sesión único de Azure AD con TigerText Secure Messenger, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="aa69d-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="aa69d-149">En Azure Portal, en la página de integración de la aplicación **TigerText Secure Messenger**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="aa69d-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa69d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="aa69d-153">En la sección **Dominio y direcciones URL de TigerText Secure Messenger**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="aa69d-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Sección Dominio y direcciones URL de TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="aa69d-155">a.</span><span class="sxs-lookup"><span data-stu-id="aa69d-155">a.</span></span> <span data-ttu-id="aa69d-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL como: `https://home.tigertext.com`.</span><span class="sxs-lookup"><span data-stu-id="aa69d-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="aa69d-157">b.</span><span class="sxs-lookup"><span data-stu-id="aa69d-157">b.</span></span> <span data-ttu-id="aa69d-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="aa69d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa69d-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="aa69d-159">This value is not real.</span></span> <span data-ttu-id="aa69d-160">Actualícelo con el identificador real.</span><span class="sxs-lookup"><span data-stu-id="aa69d-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="aa69d-161">Póngase en contacto con el [equipo de soporte técnico de TigerText Secure Messenger](mailTo:prosupport@tigertext.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="aa69d-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="aa69d-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aa69d-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="aa69d-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aa69d-164">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa69d-166">Para configurar SSO en su aplicación, póngase en contacto con el [equipo de soporte técnico de TigerText Secure Messenger](mailTo:prosupport@tigertext.com) y proporciónele los **metadatos descargados**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="aa69d-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa69d-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa69d-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="aa69d-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa69d-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa69d-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="aa69d-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-170">Create an Azure AD test user</span></span>
<span data-ttu-id="aa69d-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa69d-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="aa69d-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="aa69d-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa69d-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa69d-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa69d-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa69d-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa69d-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="aa69d-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo usuario](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa69d-182">a.</span><span class="sxs-lookup"><span data-stu-id="aa69d-182">a.</span></span> <span data-ttu-id="aa69d-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa69d-184">b.</span><span class="sxs-lookup"><span data-stu-id="aa69d-184">b.</span></span> <span data-ttu-id="aa69d-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa69d-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa69d-186">c.</span><span class="sxs-lookup"><span data-stu-id="aa69d-186">c.</span></span> <span data-ttu-id="aa69d-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa69d-188">d.</span><span class="sxs-lookup"><span data-stu-id="aa69d-188">d.</span></span> <span data-ttu-id="aa69d-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="aa69d-190">Creación de un usuario de prueba de TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="aa69d-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="aa69d-191">En esta sección, creará un usuario llamado Britta Simon en TigerText.</span><span class="sxs-lookup"><span data-stu-id="aa69d-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="aa69d-192">Póngase en contacto con el [equipo de soporte técnico de TigerText Secure Messenger](mailTo:prosupport@tigertext.com) para agregar los usuarios a la plataforma de TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="aa69d-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="aa69d-193">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa69d-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="aa69d-194">En esta sección, puede habilitar a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="aa69d-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="aa69d-196">**Para asignar a Britta Simon a TigerText Secure Messenger, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="aa69d-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="aa69d-197">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aa69d-199">En la lista de aplicaciones, seleccione **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger en la lista de aplicaciones](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="aa69d-201">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="aa69d-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-203">Click **Add** button.</span></span> <span data-ttu-id="aa69d-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="aa69d-206">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="aa69d-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa69d-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa69d-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa69d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="aa69d-209">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="aa69d-209">Test single sign-on</span></span>

<span data-ttu-id="aa69d-210">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa69d-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aa69d-211">Al hacer clic en el icono de TigerText en el panel de acceso, debería iniciar sesión automáticamente en la aplicación TigerText.</span><span class="sxs-lookup"><span data-stu-id="aa69d-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="aa69d-212">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa69d-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa69d-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aa69d-213">Additional resources</span></span>

* [<span data-ttu-id="aa69d-214">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa69d-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa69d-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa69d-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

