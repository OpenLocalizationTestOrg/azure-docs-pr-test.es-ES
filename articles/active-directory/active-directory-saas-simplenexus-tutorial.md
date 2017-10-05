---
title: "Tutorial: integración de Azure Active Directory con SimpleNexus | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SimpleNexus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bddd82b986039cf67827cb407f500edb2000964b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="e1320-103">Tutorial: Integración de Azure Active Directory con SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="e1320-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="e1320-104">En este tutorial, aprenderá a integrar SimpleNexus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1320-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1320-105">Integrar SimpleNexus con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e1320-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1320-106">Puede controlar en Azure AD quién tiene acceso a SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="e1320-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="e1320-107">Puede permitir que los usuarios inicien sesión automáticamente en SimpleNexus (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1320-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e1320-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1320-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1320-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1320-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e1320-110">Prerequisites</span></span>

<span data-ttu-id="e1320-111">Para configurar la integración de Azure AD con SimpleNexus, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e1320-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="e1320-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1320-113">Una suscripción habilitada para el inicio de sesión único en SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="e1320-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1320-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e1320-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1320-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e1320-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1320-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e1320-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1320-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1320-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1320-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e1320-118">Scenario description</span></span>
<span data-ttu-id="e1320-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e1320-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1320-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e1320-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1320-121">Incorporación de SimpleNexus desde la galería</span><span class="sxs-lookup"><span data-stu-id="e1320-121">Adding SimpleNexus from the gallery</span></span>
2. <span data-ttu-id="e1320-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="e1320-123">Incorporación de SimpleNexus desde la galería</span><span class="sxs-lookup"><span data-stu-id="e1320-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="e1320-124">Para configurar la integración de SimpleNexus en Azure AD, será preciso que agregue SimpleNexus desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e1320-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1320-125">**Para agregar SimpleNexus desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1320-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1320-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1320-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1320-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e1320-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1320-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e1320-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e1320-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1320-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e1320-133">En el cuadro de búsqueda, escriba **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="e1320-133">In the search box, type **SimpleNexus**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="e1320-135">En el panel de resultados, seleccione **SimpleNexus** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1320-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1320-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1320-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SimpleNexus con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1320-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1320-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SimpleNexus para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1320-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="e1320-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="e1320-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="e1320-141">Para establecer la relación de vínculo, en SimpleNexus, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e1320-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1320-142">Para configurar y probar el inicio de sesión único de Azure AD con SimpleNexus, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e1320-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1320-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e1320-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1320-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1320-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1320-145">**[Creación de un usuario de prueba de SimpleNexus](#creating-a-simplenexus-test-user)**: para tener un homólogo de Britta Simon en SimpleNexus que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1320-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1320-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1320-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1320-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e1320-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1320-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1320-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="e1320-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="e1320-150">**Para configurar el inicio de sesión único de Azure AD con SimpleNexus, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1320-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="e1320-151">En Azure Portal, en la página de integración de la aplicación **SimpleNexus**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e1320-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e1320-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1320-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="e1320-155">En la sección **Dominio y direcciones URL de SimpleNexus**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1320-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="e1320-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1320-157">a.</span></span> <span data-ttu-id="e1320-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://simplenexus.com/<companyname>_login`.</span><span class="sxs-lookup"><span data-stu-id="e1320-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="e1320-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1320-159">b.</span></span> <span data-ttu-id="e1320-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="e1320-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1320-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e1320-161">These values are not real.</span></span> <span data-ttu-id="e1320-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e1320-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1320-163">Póngase en contacto con el [equipo de soporte al cliente de SimpleNexus](https://simplenexus.com/site/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e1320-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="e1320-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e1320-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="e1320-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e1320-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1320-168">Para configurar el inicio de sesión único en el lado de **SimpleNexus**, es preciso enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="e1320-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="e1320-169">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="e1320-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e1320-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1320-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1320-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e1320-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1320-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1320-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1320-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1320-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1320-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e1320-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e1320-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1320-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1320-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1320-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e1320-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1320-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1320-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1320-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e1320-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1320-185">a.</span><span class="sxs-lookup"><span data-stu-id="e1320-185">a.</span></span> <span data-ttu-id="e1320-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1320-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1320-187">b.</span><span class="sxs-lookup"><span data-stu-id="e1320-187">b.</span></span> <span data-ttu-id="e1320-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1320-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1320-189">c.</span><span class="sxs-lookup"><span data-stu-id="e1320-189">c.</span></span> <span data-ttu-id="e1320-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e1320-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1320-191">d.</span><span class="sxs-lookup"><span data-stu-id="e1320-191">d.</span></span> <span data-ttu-id="e1320-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e1320-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="e1320-193">Creación de un usuario de prueba de SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="e1320-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="e1320-194">Para permitir que los usuarios de Azure AD inicien sesión en SimpleNexus, deben aprovisionarse en SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="e1320-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="e1320-195">En el caso de SimpleNexus, el aprovisionamiento es una tarea manual que realiza el Administrador de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1320-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="e1320-196">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SimpleNexus ofrecida por SimpleNexus para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="e1320-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e1320-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1320-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e1320-198">En esta sección, concederá acceso a Britta Simon a SimpleNexus para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1320-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e1320-200">**Para asignar Britta Simon a SimpleNexus, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e1320-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="e1320-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e1320-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e1320-203">En la lista de aplicaciones, seleccione **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="e1320-203">In the applications list, select **SimpleNexus**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="e1320-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e1320-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e1320-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e1320-207">Click **Add** button.</span></span> <span data-ttu-id="e1320-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e1320-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e1320-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e1320-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1320-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e1320-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1320-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e1320-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1320-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e1320-213">Testing single sign-on</span></span>

<span data-ttu-id="e1320-214">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1320-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1320-215">Al hacer clic en el icono de SimpleNexus en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="e1320-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1320-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e1320-216">Additional resources</span></span>

* [<span data-ttu-id="e1320-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1320-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1320-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1320-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

