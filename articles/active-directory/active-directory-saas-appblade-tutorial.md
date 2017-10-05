---
title: "Tutorial: Integración de Azure Active Directory con AppBlade | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 7820a70b34b6d25ba81b17c472159d08904335d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="f45dc-103">Tutorial: Integración de Azure Active Directory con AppBlade</span><span class="sxs-lookup"><span data-stu-id="f45dc-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="f45dc-104">En este tutorial, obtendrá información sobre cómo integrar AppBlade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f45dc-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f45dc-105">La integración de AppBlade con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f45dc-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f45dc-106">Puede controlar en Azure AD quién tiene acceso a AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="f45dc-107">Puede permitir que los usuarios inicien sesión automáticamente en AppBlade (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f45dc-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f45dc-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f45dc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f45dc-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f45dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f45dc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f45dc-110">Prerequisites</span></span>

<span data-ttu-id="f45dc-111">Para configurar la integración de Azure AD con AppBlade, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f45dc-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="f45dc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f45dc-113">Una suscripción habilitada para inicio de sesión único en AppBlade</span><span class="sxs-lookup"><span data-stu-id="f45dc-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f45dc-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f45dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f45dc-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f45dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f45dc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f45dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f45dc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f45dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f45dc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f45dc-118">Scenario description</span></span>
<span data-ttu-id="f45dc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f45dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f45dc-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f45dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f45dc-121">Adición de AppBlade desde la galería</span><span class="sxs-lookup"><span data-stu-id="f45dc-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="f45dc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="f45dc-123">Adición de AppBlade desde la galería</span><span class="sxs-lookup"><span data-stu-id="f45dc-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="f45dc-124">Para configurar la integración de AppBlade en Azure AD, deberá agregar AppBlade desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f45dc-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f45dc-125">**Para agregar AppBlade desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f45dc-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f45dc-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f45dc-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f45dc-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f45dc-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f45dc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f45dc-133">En el cuadro de búsqueda, escriba **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-133">In the search box, type **AppBlade**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="f45dc-135">En el panel de resultados, seleccione **AppBlade** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f45dc-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f45dc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f45dc-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AppBlade con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f45dc-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f45dc-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de AppBlade para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f45dc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="f45dc-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="f45dc-141">Para establecer la relación de vínculo, en AppBlade, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f45dc-142">Para configurar y probar el inicio de sesión único de Azure AD con AppBlade, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f45dc-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f45dc-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f45dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f45dc-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f45dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f45dc-145">**[Creación de un usuario de prueba de AppBlade](#creating-an-appblade-test-user)**: para tener un homólogo de Britta Simon en AppBlade que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f45dc-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f45dc-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f45dc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f45dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f45dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f45dc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f45dc-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="f45dc-150">**Para configurar el inicio de sesión único de Azure AD con AppBlade, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f45dc-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="f45dc-151">En Azure Portal, en la página de integración de la aplicación **AppBlade**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f45dc-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f45dc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="f45dc-155">En la sección **Dominio y direcciones URL de AppBlade**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f45dc-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="f45dc-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.appblade.com/saml/<tenantid>`.</span><span class="sxs-lookup"><span data-stu-id="f45dc-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f45dc-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="f45dc-158">This value is not real.</span></span> <span data-ttu-id="f45dc-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="f45dc-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f45dc-160">Póngase en contacto con el [equipo de soporte técnico de AppBlade](mailto:support@appblade.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="f45dc-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="f45dc-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f45dc-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="f45dc-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f45dc-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f45dc-165">Para configurar el inicio de sesión único en **AppBlade**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f45dc-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="f45dc-166">Además, pídales que configuren la **URL de usuario de SSO** como `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="f45dc-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="f45dc-167">Esta configuración es necesaria para que el inicio de sesión único funcione.</span><span class="sxs-lookup"><span data-stu-id="f45dc-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="f45dc-168">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f45dc-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f45dc-169">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f45dc-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f45dc-170">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f45dc-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f45dc-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f45dc-172">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f45dc-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f45dc-174">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f45dc-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f45dc-175">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f45dc-177">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f45dc-179">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f45dc-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f45dc-181">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f45dc-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f45dc-183">a.</span><span class="sxs-lookup"><span data-stu-id="f45dc-183">a.</span></span> <span data-ttu-id="f45dc-184">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f45dc-185">b.</span><span class="sxs-lookup"><span data-stu-id="f45dc-185">b.</span></span> <span data-ttu-id="f45dc-186">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f45dc-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f45dc-187">c.</span><span class="sxs-lookup"><span data-stu-id="f45dc-187">c.</span></span> <span data-ttu-id="f45dc-188">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f45dc-189">d.</span><span class="sxs-lookup"><span data-stu-id="f45dc-189">d.</span></span> <span data-ttu-id="f45dc-190">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="f45dc-191">Creación de un usuario de prueba de AppBlade</span><span class="sxs-lookup"><span data-stu-id="f45dc-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="f45dc-192">El objetivo de esta sección es crear un usuario llamado Britta Simon en AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="f45dc-193">AppBlade admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f45dc-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f45dc-194">**Asegúrese de que el nombre de dominio está configurado con AppBlade para el aprovisionamiento de usuarios. Después de eso solo funciona el aprovisionamiento de usuarios Just-In-Time.**</span><span class="sxs-lookup"><span data-stu-id="f45dc-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="f45dc-195">Si el usuario tiene una dirección de correo electrónico que termina con el dominio configurado por AppBlade para la cuenta, dicho usuario se unirá automáticamente a la cuenta como un miembro con el nivel de permiso que especifique, que puede ser "Básico" (un usuario básico que solamente puede instalar aplicaciones), "Miembro del equipo" (un usuario que puede cargar nuevas versiones de aplicaciones y administrar proyectos) o "Administrador" (privilegios completos de administrador para la cuenta).</span><span class="sxs-lookup"><span data-stu-id="f45dc-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="f45dc-196">Normalmente se elegiría Básico y después se promocionaría a los usuarios manualmente a través de un inicio de sesión del administrador (AppBlade debe configurar un inicio de sesión del administrador basado en correo electrónico por adelantado o promocionar a un usuario en nombre del cliente después de iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="f45dc-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="f45dc-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="f45dc-197">There is no action item for you in this section.</span></span> <span data-ttu-id="f45dc-198">Durante un intento de acceder a AppBlade se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="f45dc-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="f45dc-199">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f45dc-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f45dc-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f45dc-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f45dc-201">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f45dc-203">**Para asignar a Britta Simon a AppBlade, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f45dc-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="f45dc-204">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f45dc-206">En la lista de aplicaciones, seleccione **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-206">In the applications list, select **AppBlade**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="f45dc-208">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f45dc-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-210">Click **Add** button.</span></span> <span data-ttu-id="f45dc-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f45dc-213">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f45dc-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f45dc-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f45dc-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f45dc-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f45dc-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f45dc-216">Testing single sign-on</span></span>

<span data-ttu-id="f45dc-217">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f45dc-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f45dc-218">Al hacer clic en el icono de AppBlade en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación AppBlade.</span><span class="sxs-lookup"><span data-stu-id="f45dc-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f45dc-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f45dc-219">Additional resources</span></span>

* [<span data-ttu-id="f45dc-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f45dc-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f45dc-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f45dc-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

