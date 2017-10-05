---
title: "Tutorial: Integración de Azure Active Directory con Bridge | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Bridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d2b7fd6f73f1b782cfe6337d13f9f22f9c70d389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="88878-103">Tutorial: Integración de Azure Active Directory con Bridge</span><span class="sxs-lookup"><span data-stu-id="88878-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="88878-104">En este tutorial, obtendrá información sobre cómo integrar Bridge con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88878-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88878-105">La integración de Bridge con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="88878-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88878-106">Puede controlar en Azure AD quién tiene acceso a Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="88878-107">Puede permitir que los usuarios inicien sesión automáticamente en Bridge (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88878-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88878-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="88878-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88878-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88878-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="88878-110">Prerequisites</span></span>

<span data-ttu-id="88878-111">Para configurar la integración de Azure AD con Bridge, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="88878-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="88878-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88878-113">Una suscripción habilitada para el inicio de sesión único en Bridge</span><span class="sxs-lookup"><span data-stu-id="88878-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88878-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="88878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88878-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="88878-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88878-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="88878-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88878-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88878-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="88878-118">Scenario description</span></span>
<span data-ttu-id="88878-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="88878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88878-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="88878-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88878-121">Adición de Bridge desde la galería</span><span class="sxs-lookup"><span data-stu-id="88878-121">Adding Bridge from the gallery</span></span>
2. <span data-ttu-id="88878-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-the-gallery"></a><span data-ttu-id="88878-123">Adición de Bridge desde la galería</span><span class="sxs-lookup"><span data-stu-id="88878-123">Adding Bridge from the gallery</span></span>
<span data-ttu-id="88878-124">Para configurar la integración de Bridge en Azure AD, es preciso agregar Bridge desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="88878-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88878-125">**Para agregar Bridge desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="88878-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88878-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88878-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="88878-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88878-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="88878-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="88878-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88878-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="88878-133">En el cuadro de búsqueda, escriba **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="88878-133">In the search box, type **Bridge**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="88878-135">En el panel de resultados, seleccione **Bridge** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88878-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88878-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88878-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Bridge con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88878-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88878-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Bridge para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="88878-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="88878-141">Para establecer la relación de vínculo, en Bridge, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="88878-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="88878-142">Para configurar y probar el inicio de sesión único de Azure AD con Bridge, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="88878-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88878-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="88878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88878-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88878-145">**[Creación de un usuario de prueba para Bridge](#creating-a-bridge-test-user)**: para tener un homólogo de Britta Simon en Bridge que esté vinculado a su representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88878-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88878-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88878-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="88878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88878-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88878-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="88878-150">**Para configurar el inicio de sesión único de Azure AD con Bridge, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="88878-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="88878-151">En Azure Portal, en la página de integración de la aplicación **Bridge**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="88878-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="88878-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="88878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="88878-155">En la sección **Dominio y direcciones URL de Bridge**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="88878-155">On the **Bridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="88878-157">a.</span><span class="sxs-lookup"><span data-stu-id="88878-157">a.</span></span> <span data-ttu-id="88878-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.bridgeapp.com`.</span><span class="sxs-lookup"><span data-stu-id="88878-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="88878-159">b.</span><span class="sxs-lookup"><span data-stu-id="88878-159">b.</span></span> <span data-ttu-id="88878-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="88878-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88878-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="88878-161">These values are not real.</span></span> <span data-ttu-id="88878-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="88878-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="88878-163">Póngase en contacto con el [equipo de soporte de cliente de Bridge](https://community.bridgeapp.com/community/help) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="88878-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="88878-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="88878-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="88878-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="88878-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88878-168">En la sección **Configuración de Bridge**, haga clic en **Configurar Bridge** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="88878-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="88878-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="88878-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="88878-171">Para configurar el inicio de sesión único en **Bridge**, es preciso enviar los valores descargados de **Certificado (sin procesar)**, y el **identificador de entidad de SAML, la dirección URL del servicio de inicio de sesión único de SAML y la dirección URL de cierre de sesión** al [equipo de soporte técnico de Bridge](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="88878-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="88878-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88878-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88878-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="88878-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88878-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88878-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88878-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="88878-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88878-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="88878-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="88878-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88878-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88878-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88878-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="88878-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88878-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88878-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88878-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="88878-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88878-187">a.</span><span class="sxs-lookup"><span data-stu-id="88878-187">a.</span></span> <span data-ttu-id="88878-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88878-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88878-189">b.</span><span class="sxs-lookup"><span data-stu-id="88878-189">b.</span></span> <span data-ttu-id="88878-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88878-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88878-191">c.</span><span class="sxs-lookup"><span data-stu-id="88878-191">c.</span></span> <span data-ttu-id="88878-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="88878-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88878-193">d.</span><span class="sxs-lookup"><span data-stu-id="88878-193">d.</span></span> <span data-ttu-id="88878-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="88878-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="88878-195">Creación de un usuario de prueba para Bridge</span><span class="sxs-lookup"><span data-stu-id="88878-195">Creating a Bridge test user</span></span>

<span data-ttu-id="88878-196">En esta sección, creará un usuario llamado Britta Simon en Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="88878-197">Trabaje con el [equipo de soporte al cliente de Bridge](https://community.bridgeapp.com/community/help) para crear un usuario en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="88878-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span></span> <span data-ttu-id="88878-198">Puede presentar la incidencia de soporte técnico con Bridge <a href="https://community.bridgeapp.com/community/help">aquí</a> para agregar los usuarios en la plataforma Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88878-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88878-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88878-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="88878-202">**Para asignar a Britta Simon a Bridge, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="88878-202">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="88878-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="88878-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="88878-205">En la lista de aplicaciones, seleccione **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="88878-205">In the applications list, select **Bridge**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="88878-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="88878-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="88878-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="88878-209">Click **Add** button.</span></span> <span data-ttu-id="88878-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="88878-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="88878-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="88878-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88878-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="88878-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88878-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="88878-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88878-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="88878-215">Testing single sign-on</span></span>

<span data-ttu-id="88878-216">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="88878-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="88878-217">Al hacer clic en el icono de Bridge en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de Bridge.</span><span class="sxs-lookup"><span data-stu-id="88878-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88878-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="88878-218">Additional resources</span></span>

* [<span data-ttu-id="88878-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88878-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88878-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88878-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

