---
title: "Tutorial: Integración de Azure Active Directory con Wikispaces | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d01543955bdf6a274571f67eafdff5f637863d5c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="1c06f-103">Tutorial: Integración de Azure Active Directory con Wikispaces</span><span class="sxs-lookup"><span data-stu-id="1c06f-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="1c06f-104">En este tutorial, aprenderá a integrar Wikispaces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c06f-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c06f-105">La integración de Wikispaces con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1c06f-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c06f-106">Puede controlar en Azure AD quién tiene acceso a Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1c06f-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="1c06f-107">Puede permitir que los usuarios inicien sesión automáticamente en Wikispaces (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c06f-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c06f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1c06f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c06f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c06f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c06f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1c06f-110">Prerequisites</span></span>

<span data-ttu-id="1c06f-111">Para configurar la integración de Azure AD con Wikispaces, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1c06f-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="1c06f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c06f-113">Una suscripción habilitada para el inicio de sesión único en Wikispaces</span><span class="sxs-lookup"><span data-stu-id="1c06f-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c06f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1c06f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c06f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1c06f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c06f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1c06f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c06f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c06f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c06f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1c06f-118">Scenario description</span></span>
<span data-ttu-id="1c06f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1c06f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c06f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1c06f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c06f-121">Incorporación de Wikispaces desde la galería</span><span class="sxs-lookup"><span data-stu-id="1c06f-121">Adding Wikispaces from the gallery</span></span>
2. <span data-ttu-id="1c06f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="1c06f-123">Incorporación de Wikispaces desde la galería</span><span class="sxs-lookup"><span data-stu-id="1c06f-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="1c06f-124">Para configurar la integración de Wikispaces en Azure AD, será preciso que lo agregue desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1c06f-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c06f-125">**Para agregar Wikispaces desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1c06f-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c06f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c06f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c06f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1c06f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c06f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1c06f-133">En el cuadro de búsqueda, escriba **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-133">In the search box, type **Wikispaces**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="1c06f-135">En el panel de resultados, seleccione **Wikispaces** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1c06f-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c06f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c06f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Wikispaces con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1c06f-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c06f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Wikispaces para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c06f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="1c06f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1c06f-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="1c06f-141">Para establecer la relación de vínculo, en Wikispaces, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1c06f-142">Para configurar y probar el inicio de sesión único de Azure AD con Wikispaces, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1c06f-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c06f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1c06f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c06f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c06f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c06f-145">**[Creación de un usuario de prueba de Wikispaces](#creating-a-wikispaces-test-user)**: el objetivo es tener un homólogo de Britta Simon en Wikispacesque esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c06f-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c06f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c06f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c06f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1c06f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c06f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c06f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1c06f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="1c06f-150">**Para configurar el inicio de sesión único de Azure AD con Wikispaces, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1c06f-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="1c06f-151">En Azure Portal, en la página de integración de la aplicación **Wikispaces**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1c06f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1c06f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="1c06f-155">En la sección **Dominio y direcciones URL de Wikispaces**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1c06f-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="1c06f-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c06f-157">a.</span></span> <span data-ttu-id="1c06f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.wikispaces.net`.</span><span class="sxs-lookup"><span data-stu-id="1c06f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="1c06f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c06f-159">b.</span></span> <span data-ttu-id="1c06f-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1c06f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c06f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1c06f-161">These values are not real.</span></span> <span data-ttu-id="1c06f-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1c06f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1c06f-163">Póngase en contacto con el [equipo de soporte al cliente de Wikispaces](https://www.wikispaces.com/site/help) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1c06f-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

4. <span data-ttu-id="1c06f-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1c06f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="1c06f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1c06f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c06f-168">Para configurar el inicio de sesión único en el lado de **Wikispaces**, necesita enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="1c06f-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="1c06f-169">Tan pronto como se complete la configuración, recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="1c06f-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="1c06f-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1c06f-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c06f-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1c06f-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c06f-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c06f-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c06f-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c06f-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1c06f-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1c06f-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1c06f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c06f-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c06f-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c06f-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c06f-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c06f-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1c06f-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c06f-185">a.</span><span class="sxs-lookup"><span data-stu-id="1c06f-185">a.</span></span> <span data-ttu-id="1c06f-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c06f-187">b.</span><span class="sxs-lookup"><span data-stu-id="1c06f-187">b.</span></span> <span data-ttu-id="1c06f-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c06f-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c06f-189">c.</span><span class="sxs-lookup"><span data-stu-id="1c06f-189">c.</span></span> <span data-ttu-id="1c06f-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c06f-191">d.</span><span class="sxs-lookup"><span data-stu-id="1c06f-191">d.</span></span> <span data-ttu-id="1c06f-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="1c06f-193">Creación de un usuario de prueba de Wikispaces</span><span class="sxs-lookup"><span data-stu-id="1c06f-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="1c06f-194">Para permitir que los usuarios de Azure AD inicien sesión en Wikispaces, deben aprovisionarse en Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1c06f-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="1c06f-195">En el caso de Wikispaces, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1c06f-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="1c06f-196">Para aprovisionar cuentas de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1c06f-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="1c06f-197">Inicie sesión en su sitio de la compañía de **Wikispaces** como administrador.</span><span class="sxs-lookup"><span data-stu-id="1c06f-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="1c06f-198">Vaya a **Miembros**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="1c06f-199">![Miembros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Miembros")</span><span class="sxs-lookup"><span data-stu-id="1c06f-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="1c06f-200">Haga clic en **Invitar asistentes**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="1c06f-201">![Invitar a personas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="1c06f-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="1c06f-202">En la sección **Invitar asistentes** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1c06f-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1c06f-203">![Invitar a personas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="1c06f-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="1c06f-204">a.</span><span class="sxs-lookup"><span data-stu-id="1c06f-204">a.</span></span> <span data-ttu-id="1c06f-205">Escriba los **nombres de usuario o dirección de correo electrónico** de una cuenta válida de AAD que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="1c06f-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="1c06f-206">b.</span><span class="sxs-lookup"><span data-stu-id="1c06f-206">b.</span></span> <span data-ttu-id="1c06f-207">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="1c06f-208">El titular de la cuenta de Azure Active Directory recibe un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="1c06f-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="1c06f-209">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Wikispaces ofrecida por Wikispaces para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="1c06f-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c06f-210">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c06f-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c06f-211">En esta sección, concederá acceso a Britta Simon a Wikispaces para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c06f-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1c06f-213">**Para asignar a Britta Simon a Wikispaces, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1c06f-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="1c06f-214">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1c06f-216">En la lista de aplicaciones, seleccione **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-216">In the applications list, select **Wikispaces**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="1c06f-218">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1c06f-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-220">Click **Add** button.</span></span> <span data-ttu-id="1c06f-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1c06f-223">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1c06f-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c06f-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c06f-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1c06f-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c06f-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1c06f-226">Testing single sign-on</span></span>

<span data-ttu-id="1c06f-227">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1c06f-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1c06f-228">Al hacer clic en el icono de Wikispaces en el panel de acceso, debe iniciar sesión automáticamente en su aplicación de Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1c06f-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="1c06f-229">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c06f-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c06f-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1c06f-230">Additional resources</span></span>

* [<span data-ttu-id="1c06f-231">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c06f-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c06f-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c06f-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

