---
title: "Tutorial: Integración de Azure Active Directory con CS Stars | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y CS Stars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: acc9160f86e58c7af4779a8bab5627dc5c5ad721
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="df34e-103">Tutorial: Integración de Azure Active Directory con CS Stars</span><span class="sxs-lookup"><span data-stu-id="df34e-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="df34e-104">En este tutorial, aprenderá a integrar CS Stars con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df34e-104">In this tutorial, you learn how to integrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df34e-105">Integrar CS Stars con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="df34e-105">Integrating CS Stars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df34e-106">Puede controlar en Azure AD quién tiene acceso a CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-106">You can control in Azure AD who has access to CS Stars</span></span>
- <span data-ttu-id="df34e-107">Puede permitir que los usuarios inicien sesión automáticamente en CS Stars (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df34e-107">You can enable your users to automatically get signed-on to CS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df34e-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="df34e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="df34e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df34e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df34e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="df34e-110">Prerequisites</span></span>

<span data-ttu-id="df34e-111">Para configurar la integración de Azure AD con CS Stars, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="df34e-111">To configure Azure AD integration with CS Stars, you need the following items:</span></span>

- <span data-ttu-id="df34e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df34e-113">Una suscripción habilitada para el inicio de sesión único en CS Stars</span><span class="sxs-lookup"><span data-stu-id="df34e-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df34e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="df34e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df34e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="df34e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df34e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="df34e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df34e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df34e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df34e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="df34e-118">Scenario description</span></span>
<span data-ttu-id="df34e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="df34e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df34e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="df34e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df34e-121">Adición de CS Stars desde la galería</span><span class="sxs-lookup"><span data-stu-id="df34e-121">Adding CS Stars from the gallery</span></span>
2. <span data-ttu-id="df34e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-the-gallery"></a><span data-ttu-id="df34e-123">Adición de CS Stars desde la galería</span><span class="sxs-lookup"><span data-stu-id="df34e-123">Adding CS Stars from the gallery</span></span>
<span data-ttu-id="df34e-124">Para configurar la integración de CS Stars en Azure AD, deberá agregar CS Stars desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="df34e-124">To configure the integration of CS Stars into Azure AD, you need to add CS Stars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df34e-125">**Para agregar CS Stars desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="df34e-125">**To add CS Stars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df34e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df34e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df34e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="df34e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df34e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="df34e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="df34e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df34e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="df34e-133">En el cuadro de búsqueda, escriba **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="df34e-133">In the search box, type **CS Stars**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="df34e-135">En el panel de resultados, seleccione **CS Stars** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df34e-135">In the results panel, select **CS Stars**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df34e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df34e-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con CS Stars con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df34e-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df34e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de CS Stars para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df34e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CS Stars is to a user in Azure AD.</span></span> <span data-ttu-id="df34e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-140">In other words, a link relationship between an Azure AD user and the related user in CS Stars needs to be established.</span></span>

<span data-ttu-id="df34e-141">Para establecer la relación de vínculo, en CS Stars, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="df34e-141">In CS Stars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="df34e-142">Para configurar y probar el inicio de sesión único de Azure AD con CS Stars, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="df34e-142">To configure and test Azure AD single sign-on with CS Stars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df34e-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="df34e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df34e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df34e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df34e-145">**[Creación de un usuario de prueba de CS Stars](#creating-a-cs-stars-test-user)**: para tener un homólogo de Britta Simon en CS Stars que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df34e-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - to have a counterpart of Britta Simon in CS Stars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="df34e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df34e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df34e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="df34e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df34e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df34e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="df34e-150">**Para configurar el inicio de sesión único de Azure AD con CS Stars, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="df34e-150">**To configure Azure AD single sign-on with CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="df34e-151">En Azure Portal, en la página de integración de la aplicación **CS Stars**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="df34e-151">In the Azure portal, on the **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="df34e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="df34e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="df34e-155">En la sección **Dominio y direcciones URL de CS Stars**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="df34e-155">On the **CS Stars Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="df34e-157">a.</span><span class="sxs-lookup"><span data-stu-id="df34e-157">a.</span></span> <span data-ttu-id="df34e-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`.</span><span class="sxs-lookup"><span data-stu-id="df34e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="df34e-159">b.</span><span class="sxs-lookup"><span data-stu-id="df34e-159">b.</span></span> <span data-ttu-id="df34e-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="df34e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df34e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="df34e-161">These values are not real.</span></span> <span data-ttu-id="df34e-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="df34e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="df34e-163">Póngase en contacto con el [equipo de soporte técnico de cliente de CS Stars](http://www.marshclearsight.com/support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="df34e-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="df34e-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="df34e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="df34e-166">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="df34e-166">Click **Save** button.</span></span>

    <span data-ttu-id="df34e-167">![Configuración del inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="df34e-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="df34e-168">Para configurar el inicio de sesión único en **CS Stars**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de CS Stars](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="df34e-168">To configure single sign-on on **CS Stars** side, you need to send the downloaded **Metadata XML** to [CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="df34e-169">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df34e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="df34e-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="df34e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="df34e-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df34e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df34e-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="df34e-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df34e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="df34e-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="df34e-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df34e-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df34e-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df34e-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="df34e-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df34e-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df34e-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df34e-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="df34e-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df34e-184">a.</span><span class="sxs-lookup"><span data-stu-id="df34e-184">a.</span></span> <span data-ttu-id="df34e-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df34e-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df34e-186">b.</span><span class="sxs-lookup"><span data-stu-id="df34e-186">b.</span></span> <span data-ttu-id="df34e-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df34e-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df34e-188">c.</span><span class="sxs-lookup"><span data-stu-id="df34e-188">c.</span></span> <span data-ttu-id="df34e-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="df34e-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df34e-190">d.</span><span class="sxs-lookup"><span data-stu-id="df34e-190">d.</span></span> <span data-ttu-id="df34e-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="df34e-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="df34e-192">Creación de un usuario de prueba de CS Stars</span><span class="sxs-lookup"><span data-stu-id="df34e-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="df34e-193">El objetivo de esta sección es crear una usuaria de prueba llamada Britta Simon en CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-193">The objective of this section is to create a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="df34e-194">Para obtener un usuario creado en CS Stars, debe ponerse en contacto con el [equipo de soporte técnico de CS Stars](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="df34e-194">To get a user created in CS Stars, you need to contact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="df34e-195">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="df34e-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="df34e-196">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CS Stars.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="df34e-198">**Para asignar a Britta Simon a CS Stars, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="df34e-198">**To assign Britta Simon to CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="df34e-199">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="df34e-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="df34e-201">En la lista de aplicaciones, seleccione **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="df34e-201">In the applications list, select **CS Stars**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="df34e-203">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="df34e-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="df34e-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="df34e-205">Click **Add** button.</span></span> <span data-ttu-id="df34e-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="df34e-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="df34e-208">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="df34e-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df34e-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="df34e-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df34e-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="df34e-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df34e-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="df34e-211">Testing single sign-on</span></span>

<span data-ttu-id="df34e-212">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="df34e-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="df34e-213">Al hacer clic en el icono de CS Stars en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación CS Stars.</span><span class="sxs-lookup"><span data-stu-id="df34e-213">When you click the CS Stars tile in the Access Panel, you should get automatically signed-on to your CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="df34e-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="df34e-214">Additional resources</span></span>

* [<span data-ttu-id="df34e-215">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df34e-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df34e-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df34e-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

