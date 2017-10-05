---
title: "Tutorial: integración de Azure Active Directory con Expensify | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="b7eb7-103">Tutorial: Integración de Azure Active Directory con Expensify</span><span class="sxs-lookup"><span data-stu-id="b7eb7-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="b7eb7-104">En este tutorial, obtendrá información sobre cómo integrar Expensify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7eb7-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7eb7-105">Integrar Expensify con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7eb7-106">Puede controlar en Azure AD quién tiene acceso a Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="b7eb7-107">Puede permitir que los usuarios inicien sesión automáticamente en Expensify (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7eb7-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b7eb7-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7eb7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7eb7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b7eb7-110">Prerequisites</span></span>

<span data-ttu-id="b7eb7-111">Para configurar la integración de Azure AD con Expensify, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="b7eb7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7eb7-113">Una suscripción habilitada para el inicio de sesión único en Expensify</span><span class="sxs-lookup"><span data-stu-id="b7eb7-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7eb7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7eb7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7eb7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7eb7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7eb7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7eb7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b7eb7-118">Scenario description</span></span>
<span data-ttu-id="b7eb7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7eb7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7eb7-121">Agregar Expensify desde la galería</span><span class="sxs-lookup"><span data-stu-id="b7eb7-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="b7eb7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="b7eb7-123">Agregar Expensify desde la galería</span><span class="sxs-lookup"><span data-stu-id="b7eb7-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="b7eb7-124">Para configurar la integración de Expensify en Azure AD, deberá agregar Expensify desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7eb7-125">**Para agregar Expensify desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b7eb7-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7eb7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7eb7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b7eb7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b7eb7-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b7eb7-133">En el cuadro de búsqueda, escriba **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-133">In the search box, type **Expensify**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="b7eb7-135">En el panel de resultados, seleccione **Expensify** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7eb7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b7eb7-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Expensify con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7eb7-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7eb7-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Expensify para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="b7eb7-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="b7eb7-141">Para establecer la relación de vínculo, en Expensify, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b7eb7-142">Para configurar y probar el inicio de sesión único de Azure AD con Expensify, necesita completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7eb7-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7eb7-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7eb7-145">**[Creación de un usuario de prueba de Expensify](#creating-an-expensify-test-user)**: para tener un homólogo de Britta Simon en Expensify que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7eb7-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7eb7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7eb7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7eb7-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="b7eb7-150">**Para configurar el inicio de sesión único de Azure AD con Expensify, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b7eb7-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="b7eb7-151">En Azure Portal, en la página de integración de la aplicación **Expensify**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b7eb7-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="b7eb7-155">En la sección **Dominio y direcciones URL de Expensify**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="b7eb7-157">a.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-157">a.</span></span> <span data-ttu-id="b7eb7-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://www.expensify.com/authentication/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="b7eb7-159">b.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-159">b.</span></span> <span data-ttu-id="b7eb7-160">En el cuadro de texto **URL del identificador**, escriba una dirección URL con el siguiente patrón: `https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="b7eb7-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="b7eb7-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-161">These values are not real.</span></span> <span data-ttu-id="b7eb7-162">Debe actualizarlos con la dirección URL de inicio de sesión y del identificador real.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="b7eb7-163">Póngase en contacto con el [equipo de soporte técnico de cliente de Expensify](mailto:help@expensify.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b7eb7-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="b7eb7-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b7eb7-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7eb7-168">Para habilitar SSO en Expensify, primero deberá habilitar el **control de dominio** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="b7eb7-169">Se puede habilitar el control de dominio de la aplicación mediante los pasos enumerados [aquí](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="b7eb7-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="b7eb7-170">Para más información, trabaje con el [equipo de soporte técnico de cliente de Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="b7eb7-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="b7eb7-171">Una vez habilitado el control de dominio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="b7eb7-173">a.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-173">a.</span></span> <span data-ttu-id="b7eb7-174">Inicie sesión en la aplicación Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="b7eb7-175">b.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-175">b.</span></span> <span data-ttu-id="b7eb7-176">En la barra de herramientas de la parte superior, haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="b7eb7-177">c.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-177">c.</span></span> <span data-ttu-id="b7eb7-178">En el panel izquierdo, haga clic en **Dominio**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="b7eb7-179">d.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-179">d.</span></span> <span data-ttu-id="b7eb7-180">Haga clic en su nombre de dominio comprobado.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="b7eb7-181">e.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-181">e.</span></span> <span data-ttu-id="b7eb7-182">En el panel izquierdo, haga clic en **SAML** y, a continuación, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="b7eb7-183">f.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-183">f.</span></span> <span data-ttu-id="b7eb7-184">Abra el documento de metadatos de federación descargado desde Azure AD en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto **Metadatos del proveedor de identidades** que se proporciona.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="b7eb7-185">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b7eb7-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b7eb7-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7eb7-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7eb7-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b7eb7-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7eb7-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b7eb7-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b7eb7-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7eb7-192">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7eb7-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7eb7-196">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7eb7-198">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b7eb7-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7eb7-200">a.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-200">a.</span></span> <span data-ttu-id="b7eb7-201">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7eb7-202">b.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-202">b.</span></span> <span data-ttu-id="b7eb7-203">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7eb7-204">c.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-204">c.</span></span> <span data-ttu-id="b7eb7-205">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b7eb7-206">d.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-206">d.</span></span> <span data-ttu-id="b7eb7-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="b7eb7-208">Creación de un usuario de prueba de Expensify</span><span class="sxs-lookup"><span data-stu-id="b7eb7-208">Creating an Expensify test user</span></span>

<span data-ttu-id="b7eb7-209">En esta sección, creará un usuario denominado Britta Simon en Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="b7eb7-210">Colabore con el [equipo de soporte técnico de cliente de Expensify](mailto:help@expensify.com) para agregar los usuarios a la plataforma de Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b7eb7-211">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7eb7-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b7eb7-212">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b7eb7-214">**Para asignar a Britta Simon a Expensify, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b7eb7-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="b7eb7-215">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b7eb7-217">En la lista de aplicaciones, seleccione **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-217">In the applications list, select **Expensify**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="b7eb7-219">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b7eb7-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-221">Click **Add** button.</span></span> <span data-ttu-id="b7eb7-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b7eb7-224">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b7eb7-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7eb7-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7eb7-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b7eb7-227">Testing single sign-on</span></span>

<span data-ttu-id="b7eb7-228">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="b7eb7-229">Al hacer clic en el icono de Expensify en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Expensify.</span><span class="sxs-lookup"><span data-stu-id="b7eb7-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7eb7-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b7eb7-230">Additional resources</span></span>

* [<span data-ttu-id="b7eb7-231">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7eb7-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7eb7-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7eb7-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

