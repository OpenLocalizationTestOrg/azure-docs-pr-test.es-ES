---
title: "Tutorial: Integración de Azure Active Directory con SmarterU | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="705dd-103">Tutorial: integración de Azure Active Directory con SmarterU</span><span class="sxs-lookup"><span data-stu-id="705dd-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="705dd-104">En este tutorial, aprenderá a integrar SmarterU con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="705dd-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="705dd-105">La integración de SmarterU con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="705dd-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="705dd-106">Puede controlar en Azure AD quién tiene acceso a SmarterU</span><span class="sxs-lookup"><span data-stu-id="705dd-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="705dd-107">Puede habilitar a los usuarios para que inicien sesión automáticamente en SmarterU (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="705dd-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="705dd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="705dd-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="705dd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="705dd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="705dd-110">Prerequisites</span></span>

<span data-ttu-id="705dd-111">Para configurar la integración de Azure AD con SmarterU, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="705dd-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="705dd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="705dd-113">Una suscripción habilitada para el inicio de sesión único en SmarterU</span><span class="sxs-lookup"><span data-stu-id="705dd-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="705dd-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="705dd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="705dd-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="705dd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="705dd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="705dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="705dd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="705dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="705dd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="705dd-118">Scenario description</span></span>
<span data-ttu-id="705dd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="705dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="705dd-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="705dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="705dd-121">Incorporación de SmarterU desde la galería</span><span class="sxs-lookup"><span data-stu-id="705dd-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="705dd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="705dd-123">Incorporación de SmarterU desde la galería</span><span class="sxs-lookup"><span data-stu-id="705dd-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="705dd-124">Para configurar la integración de SmarterU en Azure AD, es preciso agregar SmarterU desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="705dd-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="705dd-125">**Para agregar SmarterU desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="705dd-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="705dd-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="705dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="705dd-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="705dd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="705dd-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="705dd-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="705dd-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="705dd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="705dd-133">En el cuadro de búsqueda, escriba **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="705dd-133">In the search box, type **SmarterU**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="705dd-135">En el panel de resultados, seleccione **SmarterU** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="705dd-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="705dd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="705dd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SmarterU con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="705dd-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="705dd-139">Para que el inicio de sesión único funcione, Azure AD tiene que saber cuál es el usuario homólogo de SmarterU para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="705dd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="705dd-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SmarterU.</span><span class="sxs-lookup"><span data-stu-id="705dd-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="705dd-141">Para establecer la relación de vínculo, en SmarterU, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="705dd-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="705dd-142">Para configurar y probar el inicio de sesión único de Azure AD con SmarterU, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="705dd-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="705dd-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="705dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="705dd-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="705dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="705dd-145">**[Creación de un usuario de prueba de SmarterU](#creating-a-smarteru-test-user)**: para tener un homólogo de Britta Simon en SmarterU que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="705dd-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="705dd-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="705dd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="705dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="705dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="705dd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="705dd-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación SmarterU.</span><span class="sxs-lookup"><span data-stu-id="705dd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="705dd-150">**Para configurar el inicio de sesión único de Azure AD con SmarterU, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="705dd-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="705dd-151">En Azure Portal, en la página de integración de la aplicación **SmarterU**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="705dd-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="705dd-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="705dd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="705dd-155">En la sección **Dominio y direcciones URL de SmarterU**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="705dd-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="705dd-157">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="705dd-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="705dd-158">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="705dd-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="705dd-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="705dd-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="705dd-162">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de SmarterU como administrador.</span><span class="sxs-lookup"><span data-stu-id="705dd-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="705dd-163">En la barra de herramientas de la parte superior, haga clic en **Configuración de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="705dd-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="705dd-164">![Configuración de la cuenta](./media/active-directory-saas-smarteru-tutorial/IC777326.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="705dd-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="705dd-165">En la página de configuración de la cuenta, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="705dd-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="705dd-166">![Autorización externa](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorización externa")</span><span class="sxs-lookup"><span data-stu-id="705dd-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="705dd-167">a.</span><span class="sxs-lookup"><span data-stu-id="705dd-167">a.</span></span> <span data-ttu-id="705dd-168">Seleccione **Habilitar autorización externa**.</span><span class="sxs-lookup"><span data-stu-id="705dd-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="705dd-169">b.</span><span class="sxs-lookup"><span data-stu-id="705dd-169">b.</span></span> <span data-ttu-id="705dd-170">En la sección **Control de inicio de sesión maestro**, seleccione la pestaña **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="705dd-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="705dd-171">c.</span><span class="sxs-lookup"><span data-stu-id="705dd-171">c.</span></span> <span data-ttu-id="705dd-172">En la sección **Inicio de sesión predeterminado de usuario**, seleccione la pestaña **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="705dd-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="705dd-173">d.</span><span class="sxs-lookup"><span data-stu-id="705dd-173">d.</span></span> <span data-ttu-id="705dd-174">Seleccione **Habilitar Okta**.</span><span class="sxs-lookup"><span data-stu-id="705dd-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="705dd-175">e.</span><span class="sxs-lookup"><span data-stu-id="705dd-175">e.</span></span> <span data-ttu-id="705dd-176">Copie el contenido del archivo de metadatos descargado y luego péguelo en el cuadro de texto **Metadatos de Okta** .</span><span class="sxs-lookup"><span data-stu-id="705dd-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="705dd-177">f.</span><span class="sxs-lookup"><span data-stu-id="705dd-177">f.</span></span> <span data-ttu-id="705dd-178">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="705dd-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="705dd-179">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="705dd-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="705dd-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="705dd-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="705dd-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="705dd-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="705dd-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="705dd-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="705dd-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="705dd-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="705dd-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="705dd-186">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="705dd-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="705dd-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="705dd-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="705dd-190">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="705dd-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="705dd-192">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="705dd-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="705dd-194">a.</span><span class="sxs-lookup"><span data-stu-id="705dd-194">a.</span></span> <span data-ttu-id="705dd-195">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="705dd-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="705dd-196">b.</span><span class="sxs-lookup"><span data-stu-id="705dd-196">b.</span></span> <span data-ttu-id="705dd-197">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="705dd-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="705dd-198">c.</span><span class="sxs-lookup"><span data-stu-id="705dd-198">c.</span></span> <span data-ttu-id="705dd-199">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="705dd-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="705dd-200">d.</span><span class="sxs-lookup"><span data-stu-id="705dd-200">d.</span></span> <span data-ttu-id="705dd-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="705dd-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="705dd-202">Creación de un usuario de prueba de SmarterU</span><span class="sxs-lookup"><span data-stu-id="705dd-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="705dd-203">Para permitir que los usuarios de Azure AD inicien sesión en SmarterU, tienen que aprovisionarse en SmarterU.</span><span class="sxs-lookup"><span data-stu-id="705dd-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="705dd-204">En el caso de SmarterU, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="705dd-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="705dd-205">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="705dd-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="705dd-206">Inicie sesión en su inquilino de **SmarterU** .</span><span class="sxs-lookup"><span data-stu-id="705dd-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="705dd-207">Vaya a **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="705dd-207">Go to **Users**.</span></span>

3. <span data-ttu-id="705dd-208">En la sección del usuario, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="705dd-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="705dd-209">![Nuevo usuario](./media/active-directory-saas-smarteru-tutorial/IC777329.png "nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="705dd-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="705dd-210">a.</span><span class="sxs-lookup"><span data-stu-id="705dd-210">a.</span></span> <span data-ttu-id="705dd-211">Haga clic en **+Usuario**.</span><span class="sxs-lookup"><span data-stu-id="705dd-211">Click **+User**.</span></span>
    
    <span data-ttu-id="705dd-212">b.</span><span class="sxs-lookup"><span data-stu-id="705dd-212">b.</span></span> <span data-ttu-id="705dd-213">Escriba los valores de atributos relacionados de la cuenta de usuario de Azure AD en los siguientes cuadros de texto: **Correo electrónico principal**, **Id. de empleado**, **Contraseña**, **Comprobar contraseña**, **Nombre de pila**, **Apellidos**.</span><span class="sxs-lookup"><span data-stu-id="705dd-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="705dd-214">c.</span><span class="sxs-lookup"><span data-stu-id="705dd-214">c.</span></span> <span data-ttu-id="705dd-215">Haga clic en **Activo**.</span><span class="sxs-lookup"><span data-stu-id="705dd-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="705dd-216">d.</span><span class="sxs-lookup"><span data-stu-id="705dd-216">d.</span></span> <span data-ttu-id="705dd-217">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="705dd-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="705dd-218">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SmarterU ofrecida por SmarterU para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="705dd-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="705dd-219">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="705dd-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="705dd-220">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SmarterU.</span><span class="sxs-lookup"><span data-stu-id="705dd-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="705dd-222">**Para asignar Britta Simon a SmarterU, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="705dd-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="705dd-223">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="705dd-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="705dd-225">En la lista de aplicaciones, seleccione **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="705dd-225">In the applications list, select **SmarterU**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="705dd-227">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="705dd-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="705dd-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="705dd-229">Click **Add** button.</span></span> <span data-ttu-id="705dd-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="705dd-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="705dd-232">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="705dd-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="705dd-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="705dd-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="705dd-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="705dd-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="705dd-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="705dd-235">Testing single sign-on</span></span>

<span data-ttu-id="705dd-236">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="705dd-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="705dd-237">Al hacer clic en el icono de SmarterU en el panel de acceso, debería iniciar sesión automáticamente en la aplicación SmarterU.</span><span class="sxs-lookup"><span data-stu-id="705dd-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="705dd-238">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="705dd-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="705dd-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="705dd-239">Additional resources</span></span>

* [<span data-ttu-id="705dd-240">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="705dd-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="705dd-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="705dd-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

