---
title: "Tutorial: integración de Azure Active Directory con Concur | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="197e6-103">Tutorial: Integración de Azure Active Directory con Concur</span><span class="sxs-lookup"><span data-stu-id="197e6-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="197e6-104">En este tutorial, aprenderá a integrar Concur con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="197e6-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="197e6-105">Integrar Concur con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="197e6-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="197e6-106">En Azure AD se puede controlar quién tiene acceso a Concur</span><span class="sxs-lookup"><span data-stu-id="197e6-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="197e6-107">Puede permitir que los usuarios inicien sesión automáticamente en Concur (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="197e6-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="197e6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="197e6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="197e6-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="197e6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="197e6-110">Prerequisites</span></span>

<span data-ttu-id="197e6-111">Para configurar la integración de Azure AD con Concur, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="197e6-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="197e6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="197e6-113">Una suscripción habilitada para el inicio de sesión único en Concur</span><span class="sxs-lookup"><span data-stu-id="197e6-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="197e6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="197e6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="197e6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="197e6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="197e6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="197e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="197e6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="197e6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="197e6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="197e6-118">Scenario description</span></span>
<span data-ttu-id="197e6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="197e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="197e6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="197e6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="197e6-121">Agregar Concur desde la galería</span><span class="sxs-lookup"><span data-stu-id="197e6-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="197e6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="197e6-123">La configuración de la suscripción a Concur para un SSO federado mediante SAML es una tarea independiente. Para llevarla a cabo, debe ponerse en contacto con el [equipo de soporte al cliente de Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="197e6-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="197e6-124">Agregar Concur desde la galería</span><span class="sxs-lookup"><span data-stu-id="197e6-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="197e6-125">Para configurar la integración de Concur en Azure AD, debe agregar Concur desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="197e6-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="197e6-126">**Para agregar Concur desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="197e6-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="197e6-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="197e6-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="197e6-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="197e6-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="197e6-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="197e6-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="197e6-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="197e6-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="197e6-134">En el cuadro de búsqueda, escriba **Concur**.</span><span class="sxs-lookup"><span data-stu-id="197e6-134">In the search box, type **Concur**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="197e6-136">En el panel de resultados, seleccione **Concur** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="197e6-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="197e6-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="197e6-139">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Concur con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="197e6-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="197e6-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Concur para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="197e6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="197e6-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="197e6-142">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor de **Username** (Nombre de usuario) en Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="197e6-143">Para configurar y probar el inicio de sesión único de Azure AD con Concur, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="197e6-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="197e6-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="197e6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="197e6-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="197e6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="197e6-146">**[Creación de un usuario de prueba de Concur](#creating-a-concur-test-user)**: para tener un homólogo de Britta Simon en Concur que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="197e6-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="197e6-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="197e6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="197e6-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="197e6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="197e6-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="197e6-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="197e6-151">**Para configurar el inicio de sesión único de Azure AD con Concur, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="197e6-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="197e6-152">En Azure Portal, en la página de integración de la aplicación **Concur**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="197e6-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="197e6-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="197e6-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="197e6-156">En la sección **Dominio y direcciones URL de Concur**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="197e6-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="197e6-158">a.</span><span class="sxs-lookup"><span data-stu-id="197e6-158">a.</span></span> <span data-ttu-id="197e6-159">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="197e6-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="197e6-160">b.</span><span class="sxs-lookup"><span data-stu-id="197e6-160">b.</span></span> <span data-ttu-id="197e6-161">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="197e6-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="197e6-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="197e6-162">These values are not the real.</span></span> <span data-ttu-id="197e6-163">Actualice estos valores con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="197e6-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="197e6-164">Póngase en contacto con el [equipo de soporte al cliente de Concur](https://www.concur.co.in/contact) para obtenerlos.</span><span class="sxs-lookup"><span data-stu-id="197e6-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="197e6-165">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="197e6-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="197e6-167">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="197e6-167">Click **Save** button.</span></span>

    <span data-ttu-id="197e6-168">![Configurar el inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="197e6-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="197e6-169">Para configurar el inicio de sesión único en el lado de **Concur**, es preciso enviar los datos descargados de **XML de metadatos** al equipo de soporte técnico de Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="197e6-170">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="197e6-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="197e6-171">La configuración de la suscripción a Concur para un SSO federado mediante SAML es una tarea independiente. Para llevarla a cabo, debe ponerse en contacto con el [equipo de soporte al cliente de Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="197e6-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="197e6-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="197e6-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="197e6-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="197e6-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="197e6-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="197e6-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="197e6-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="197e6-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="197e6-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="197e6-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="197e6-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="197e6-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="197e6-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="197e6-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="197e6-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="197e6-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="197e6-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="197e6-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="197e6-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="197e6-187">a.</span><span class="sxs-lookup"><span data-stu-id="197e6-187">a.</span></span> <span data-ttu-id="197e6-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="197e6-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="197e6-189">b.</span><span class="sxs-lookup"><span data-stu-id="197e6-189">b.</span></span> <span data-ttu-id="197e6-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="197e6-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="197e6-191">c.</span><span class="sxs-lookup"><span data-stu-id="197e6-191">c.</span></span> <span data-ttu-id="197e6-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="197e6-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="197e6-193">d.</span><span class="sxs-lookup"><span data-stu-id="197e6-193">d.</span></span> <span data-ttu-id="197e6-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="197e6-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="197e6-195">Creación de un usuario de prueba de Concur</span><span class="sxs-lookup"><span data-stu-id="197e6-195">Creating a Concur test user</span></span>

<span data-ttu-id="197e6-196">La aplicación admite el aprovisionamiento de usuarios justo a tiempo y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="197e6-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="197e6-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="197e6-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="197e6-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="197e6-200">**Para asignar Britta Simon a Concur, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="197e6-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="197e6-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="197e6-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="197e6-203">En la lista de aplicaciones, seleccione **Concur**.</span><span class="sxs-lookup"><span data-stu-id="197e6-203">In the applications list, select **Concur**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="197e6-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="197e6-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="197e6-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="197e6-207">Click **Add** button.</span></span> <span data-ttu-id="197e6-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="197e6-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="197e6-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="197e6-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="197e6-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="197e6-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="197e6-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="197e6-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="197e6-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="197e6-213">Testing single sign-on</span></span>

<span data-ttu-id="197e6-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="197e6-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="197e6-215">Al hacer clic en el icono de Concur del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Concur.</span><span class="sxs-lookup"><span data-stu-id="197e6-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="197e6-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="197e6-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="197e6-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="197e6-217">Additional resources</span></span>

* [<span data-ttu-id="197e6-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="197e6-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="197e6-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="197e6-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="197e6-220">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="197e6-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

