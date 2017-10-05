---
title: "Tutorial: Integración de Azure Active Directory con Jive | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="acf45-103">Tutorial: Integración de Azure Active Directory con Jive</span><span class="sxs-lookup"><span data-stu-id="acf45-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="acf45-104">En este tutorial, obtendrá información sobre cómo integrar Jive con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acf45-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acf45-105">Integrar Jive con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="acf45-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acf45-106">Puede controlar en Azure AD quién tiene acceso a Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="acf45-107">Puede permitir que los usuarios inicien sesión automáticamente en Jive (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf45-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acf45-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="acf45-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="acf45-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acf45-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf45-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="acf45-110">Prerequisites</span></span>

<span data-ttu-id="acf45-111">Para configurar la integración de Azure AD con Jive, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="acf45-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="acf45-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acf45-113">Una suscripción habilitada para inicio de sesión único en Jive</span><span class="sxs-lookup"><span data-stu-id="acf45-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acf45-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="acf45-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acf45-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="acf45-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acf45-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="acf45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acf45-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acf45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acf45-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="acf45-118">Scenario description</span></span>
<span data-ttu-id="acf45-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="acf45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acf45-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="acf45-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acf45-121">Adición de Jive desde la galería</span><span class="sxs-lookup"><span data-stu-id="acf45-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="acf45-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="acf45-123">Adición de Jive desde la galería</span><span class="sxs-lookup"><span data-stu-id="acf45-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="acf45-124">Para configurar la integración de Jive en Azure AD, deberá agregar Jive desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="acf45-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acf45-125">**Para agregar Jive desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="acf45-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acf45-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acf45-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acf45-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="acf45-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acf45-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="acf45-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="acf45-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="acf45-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="acf45-133">En el cuadro de búsqueda, escriba **Jive**.</span><span class="sxs-lookup"><span data-stu-id="acf45-133">In the search box, type **Jive**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="acf45-135">En el panel de resultados, seleccione **Jive** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf45-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acf45-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acf45-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jive con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="acf45-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="acf45-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Jive para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf45-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="acf45-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="acf45-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="acf45-142">Para configurar y probar el inicio de sesión único de Azure AD con Jive, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="acf45-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acf45-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="acf45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="acf45-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acf45-145">**[Creación de un usuario de prueba de Jive](#creating-a-jive-test-user)**: para tener un homólogo de Britta Simon en Jive que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf45-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="acf45-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf45-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acf45-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="acf45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acf45-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acf45-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="acf45-150">**Para configurar el inicio de sesión único de Azure AD con Jive, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="acf45-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="acf45-151">En Azure Portal, en la página de integración de la aplicación **Jive**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="acf45-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="acf45-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="acf45-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="acf45-155">En la sección **Dominio y direcciones URL de Jive**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="acf45-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="acf45-157">a.</span><span class="sxs-lookup"><span data-stu-id="acf45-157">a.</span></span> <span data-ttu-id="acf45-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instance name>.jivecustom.com`.</span><span class="sxs-lookup"><span data-stu-id="acf45-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="acf45-159">b.</span><span class="sxs-lookup"><span data-stu-id="acf45-159">b.</span></span> <span data-ttu-id="acf45-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="acf45-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="acf45-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="acf45-161">These values are not the real.</span></span> <span data-ttu-id="acf45-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="acf45-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="acf45-163">Póngase en contacto con el [equipo de soporte de cliente de Jive](https://www.jivesoftware.com/services-support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="acf45-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="acf45-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="acf45-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="acf45-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="acf45-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="acf45-168">Para configurar el inicio de sesión único en **Jive**, inicie sesión en su inquilino de Jive como administrador.</span><span class="sxs-lookup"><span data-stu-id="acf45-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="acf45-169">En el menú de la parte superior, haga clic en "**Saml**".</span><span class="sxs-lookup"><span data-stu-id="acf45-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="acf45-171">a.</span><span class="sxs-lookup"><span data-stu-id="acf45-171">a.</span></span> <span data-ttu-id="acf45-172">Seleccione **Habilitado** en la pestaña **General**.</span><span class="sxs-lookup"><span data-stu-id="acf45-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="acf45-173">b.</span><span class="sxs-lookup"><span data-stu-id="acf45-173">b.</span></span> <span data-ttu-id="acf45-174">Haga clic en el botón "**Guardar toda la configuración de saml**".</span><span class="sxs-lookup"><span data-stu-id="acf45-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="acf45-175">Vaya a la pestaña "**Metadatos de IdP**".</span><span class="sxs-lookup"><span data-stu-id="acf45-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="acf45-177">a.</span><span class="sxs-lookup"><span data-stu-id="acf45-177">a.</span></span> <span data-ttu-id="acf45-178">Copie el contenido del archivo XML de metadatos descargado y, después, péguelo en el cuadro de texto **Identity Provider (IDP) Metadata** (Metadatos del proveedor de identidades [IDP]).</span><span class="sxs-lookup"><span data-stu-id="acf45-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="acf45-179">b.</span><span class="sxs-lookup"><span data-stu-id="acf45-179">b.</span></span> <span data-ttu-id="acf45-180">Haga clic en el botón "**Guardar toda la configuración de saml**".</span><span class="sxs-lookup"><span data-stu-id="acf45-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="acf45-181">Vaya a la pestaña "**User Attribute Mapping**" (Asignación de atributos de usuario).</span><span class="sxs-lookup"><span data-stu-id="acf45-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="acf45-183">a.</span><span class="sxs-lookup"><span data-stu-id="acf45-183">a.</span></span> <span data-ttu-id="acf45-184">En el cuadro de texto **Email** (Correo electrónico), copie y pegue el nombre del atributo de valor **mail**.</span><span class="sxs-lookup"><span data-stu-id="acf45-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="acf45-185">b.</span><span class="sxs-lookup"><span data-stu-id="acf45-185">b.</span></span> <span data-ttu-id="acf45-186">En el cuadro de texto **First Name** (Nombre), copie y pegue el nombre del atributo de valor **givenname**.</span><span class="sxs-lookup"><span data-stu-id="acf45-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="acf45-187">c.</span><span class="sxs-lookup"><span data-stu-id="acf45-187">c.</span></span> <span data-ttu-id="acf45-188">En el cuadro de texto **Last Name** (Apellidos), copie y pegue el nombre del atributo de valor **surname**.</span><span class="sxs-lookup"><span data-stu-id="acf45-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="acf45-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf45-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="acf45-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="acf45-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="acf45-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acf45-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acf45-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="acf45-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="acf45-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="acf45-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="acf45-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acf45-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acf45-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acf45-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="acf45-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acf45-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="acf45-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acf45-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="acf45-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acf45-204">a.</span><span class="sxs-lookup"><span data-stu-id="acf45-204">a.</span></span> <span data-ttu-id="acf45-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acf45-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acf45-206">b.</span><span class="sxs-lookup"><span data-stu-id="acf45-206">b.</span></span> <span data-ttu-id="acf45-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf45-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acf45-208">c.</span><span class="sxs-lookup"><span data-stu-id="acf45-208">c.</span></span> <span data-ttu-id="acf45-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="acf45-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="acf45-210">d.</span><span class="sxs-lookup"><span data-stu-id="acf45-210">d.</span></span> <span data-ttu-id="acf45-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="acf45-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="acf45-212">Creación de un usuario de prueba de Jive</span><span class="sxs-lookup"><span data-stu-id="acf45-212">Creating a Jive test user</span></span>

<span data-ttu-id="acf45-213">Trabaje con el [equipo de soporte técnico del cliente de Jive](https://www.jivesoftware.com/services-support/) para agregar los usuarios a la plataforma de Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="acf45-214">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf45-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="acf45-215">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="acf45-217">**Para asignar a Britta Simon a Jive, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="acf45-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="acf45-218">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="acf45-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="acf45-220">En la lista de aplicaciones, seleccione **Jive**.</span><span class="sxs-lookup"><span data-stu-id="acf45-220">In the applications list, select **Jive**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="acf45-222">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="acf45-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="acf45-224">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="acf45-224">Click **Add** button.</span></span> <span data-ttu-id="acf45-225">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="acf45-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="acf45-227">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="acf45-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="acf45-228">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="acf45-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acf45-229">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="acf45-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="acf45-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="acf45-230">Testing single sign-on</span></span>

<span data-ttu-id="acf45-231">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="acf45-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acf45-232">Al hacer clic en el icono de Jive en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Jive.</span><span class="sxs-lookup"><span data-stu-id="acf45-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="acf45-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="acf45-233">Additional resources</span></span>

* [<span data-ttu-id="acf45-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acf45-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acf45-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acf45-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="acf45-236">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="acf45-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

