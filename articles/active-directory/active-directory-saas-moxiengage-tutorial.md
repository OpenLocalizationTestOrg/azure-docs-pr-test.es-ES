---
title: "Tutorial: integración de Azure Active Directory con Moxi Engage | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Moxi Engage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 25b5e377d8d0d504860ab9a8c4dac49c9ca5b104
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a><span data-ttu-id="0f01c-103">Tutorial: integración de Azure Active Directory con Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="0f01c-103">Tutorial: Azure Active Directory integration with Moxi Engage</span></span>

<span data-ttu-id="0f01c-104">En este tutorial, aprenderá a integrar Moxi Engage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f01c-104">In this tutorial, you learn how to integrate Moxi Engage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f01c-105">La integración de Moxi Engage con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0f01c-105">Integrating Moxi Engage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0f01c-106">Puede controlar en Azure AD quién tiene acceso a Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-106">You can control in Azure AD who has access to Moxi Engage</span></span>
- <span data-ttu-id="0f01c-107">Puede habilitar que los usuarios inicien sesión automáticamente en Moxi Engage (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f01c-107">You can enable your users to automatically get signed-on to Moxi Engage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f01c-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0f01c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0f01c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f01c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f01c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0f01c-110">Prerequisites</span></span>

<span data-ttu-id="0f01c-111">Para configurar la integración de Azure AD con Moxi Engage, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0f01c-111">To configure Azure AD integration with Moxi Engage, you need the following items:</span></span>

- <span data-ttu-id="0f01c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f01c-113">Una suscripción habilitada para inicio de sesión único en Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="0f01c-113">A Moxi Engage single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f01c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0f01c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f01c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0f01c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f01c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0f01c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f01c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f01c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f01c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0f01c-118">Scenario description</span></span>
<span data-ttu-id="0f01c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0f01c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f01c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0f01c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f01c-121">Incorporación de Moxi Engage desde la galería</span><span class="sxs-lookup"><span data-stu-id="0f01c-121">Adding Moxi Engage from the gallery</span></span>
2. <span data-ttu-id="0f01c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxi-engage-from-the-gallery"></a><span data-ttu-id="0f01c-123">Incorporación de Moxi Engage desde la galería</span><span class="sxs-lookup"><span data-stu-id="0f01c-123">Adding Moxi Engage from the gallery</span></span>
<span data-ttu-id="0f01c-124">Para configurar la integración de Moxi Engage en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0f01c-124">To configure the integration of Moxi Engage into Azure AD, you need to add Moxi Engage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0f01c-125">**Para agregar Moxi Engage desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0f01c-125">**To add Moxi Engage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0f01c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f01c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0f01c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0f01c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0f01c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0f01c-133">En el cuadro de búsqueda, escriba **Moxi Engage**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-133">In the search box, type **Moxi Engage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_search.png)

5. <span data-ttu-id="0f01c-135">En el panel de resultados, seleccione **Moxi Engage** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f01c-135">In the results panel, select **Moxi Engage**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f01c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f01c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Moxi Engage con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f01c-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0f01c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Moxi Engage para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f01c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxi Engage is to a user in Azure AD.</span></span> <span data-ttu-id="0f01c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-140">In other words, a link relationship between an Azure AD user and the related user in Moxi Engage needs to be established.</span></span>

<span data-ttu-id="0f01c-141">Para establecer la relación de vínculo, en Moxi Engage, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-141">In Moxi Engage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0f01c-142">Para configurar y probar el inicio de sesión único de Azure AD con Moxi Engage, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0f01c-142">To configure and test Azure AD single sign-on with Moxi Engage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0f01c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0f01c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0f01c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f01c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f01c-145">**[Creación de un usuario de prueba de Moxi Engage](#creating-a-moxi-engage-test-user)**: para tener un homólogo de Britta Simon en Moxi Engage vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0f01c-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - to have a counterpart of Britta Simon in Moxi Engage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f01c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f01c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f01c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0f01c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f01c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f01c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxi Engage application.</span></span>

<span data-ttu-id="0f01c-150">**Para configurar el inicio de sesión único de Azure AD con Moxi Engage, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0f01c-150">**To configure Azure AD single sign-on with Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="0f01c-151">En Azure Portal, en la página de integración de la aplicación **Moxi Engage**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-151">In the Azure portal, on the **Moxi Engage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0f01c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0f01c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

3. <span data-ttu-id="0f01c-155">En la sección **Moxi Engage Domain and URLs** (Dominio y direcciones URL de Moxi Engage), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0f01c-155">On the **Moxi Engage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_url.png)

    <span data-ttu-id="0f01c-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`.</span><span class="sxs-lookup"><span data-stu-id="0f01c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0f01c-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="0f01c-158">This value is not real.</span></span> <span data-ttu-id="0f01c-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0f01c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0f01c-160">Póngase en contacto con el [equipo de soporte técnico de Moxi Engage](mailto:support@moxiworks.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="0f01c-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) to get this value.</span></span> 
 
4. <span data-ttu-id="0f01c-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0f01c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

5. <span data-ttu-id="0f01c-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0f01c-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxiengage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0f01c-165">Para configurar el inicio de sesión único en el lado de **Moxi Engage**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Moxi Engage](mailto:support@moxiworks.com).</span><span class="sxs-lookup"><span data-stu-id="0f01c-165">To configure single sign-on on **Moxi Engage** side, you need to send the downloaded **Metadata XML** to [Moxi Engage support team](mailto:support@moxiworks.com).</span></span> <span data-ttu-id="0f01c-166">Ellos lo configuran para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="0f01c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0f01c-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f01c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0f01c-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0f01c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0f01c-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f01c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f01c-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f01c-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0f01c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0f01c-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0f01c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0f01c-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f01c-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f01c-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0f01c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f01c-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0f01c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f01c-182">a.</span><span class="sxs-lookup"><span data-stu-id="0f01c-182">a.</span></span> <span data-ttu-id="0f01c-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f01c-184">b.</span><span class="sxs-lookup"><span data-stu-id="0f01c-184">b.</span></span> <span data-ttu-id="0f01c-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f01c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f01c-186">c.</span><span class="sxs-lookup"><span data-stu-id="0f01c-186">c.</span></span> <span data-ttu-id="0f01c-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0f01c-188">d.</span><span class="sxs-lookup"><span data-stu-id="0f01c-188">d.</span></span> <span data-ttu-id="0f01c-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-189">Click **Create**.</span></span>
 
### <a name="creating-a-moxi-engage-test-user"></a><span data-ttu-id="0f01c-190">Creación de un usuario de prueba de Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="0f01c-190">Creating a Moxi Engage test user</span></span>

<span data-ttu-id="0f01c-191">En esta sección, creará un usuario llamado Britta Simon en Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-191">In this section, you create a user called Britta Simon in Moxi Engage.</span></span> <span data-ttu-id="0f01c-192">Trabaje con el [equipo de soporte técnico de Moxi Engage](mailto:support@moxiworks.com) para agregar los usuarios a la plataforma de Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add the users in the Moxi Engage platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0f01c-193">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f01c-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0f01c-194">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxi Engage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0f01c-196">**Para asignar a Britta Simon a Moxi Engage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0f01c-196">**To assign Britta Simon to Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="0f01c-197">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0f01c-199">En la lista de aplicaciones, seleccione **Moxi Engage**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-199">In the applications list, select **Moxi Engage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_app.png) 

3. <span data-ttu-id="0f01c-201">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0f01c-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-203">Click **Add** button.</span></span> <span data-ttu-id="0f01c-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0f01c-206">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0f01c-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0f01c-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f01c-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0f01c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f01c-209">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0f01c-209">Testing single sign-on</span></span>

<span data-ttu-id="0f01c-210">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f01c-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0f01c-211">Al hacer clic en el icono de Moxi Engage en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="0f01c-211">When you click the Moxi Engage tile in the Access Panel, you should get automatic login to Moxi Engage application.</span></span>
<span data-ttu-id="0f01c-212">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f01c-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0f01c-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0f01c-213">Additional resources</span></span>

* [<span data-ttu-id="0f01c-214">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f01c-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f01c-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f01c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_203.png

