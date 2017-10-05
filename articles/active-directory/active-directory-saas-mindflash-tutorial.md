---
title: "Tutorial: Integración de Azure Active Directory con Mindflash | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="89294-103">Tutorial: Integración de Azure Active Directory con Mindflash</span><span class="sxs-lookup"><span data-stu-id="89294-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="89294-104">En este tutorial, obtendrá información sobre cómo integrar Mindflash con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89294-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89294-105">La integración de Mindflash con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="89294-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89294-106">Puede controlar en Azure AD quién tiene acceso a Mindflash</span><span class="sxs-lookup"><span data-stu-id="89294-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="89294-107">Puede permitir que los usuarios inicien sesión automáticamente en Mindflash (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89294-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="89294-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="89294-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89294-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89294-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="89294-110">Prerequisites</span></span>

<span data-ttu-id="89294-111">Para configurar la integración de Azure AD con Mindflash, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="89294-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="89294-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89294-113">Una suscripción habilitada para inicio de sesión único en Mindflash</span><span class="sxs-lookup"><span data-stu-id="89294-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89294-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="89294-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89294-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="89294-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89294-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="89294-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89294-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89294-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89294-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="89294-118">Scenario description</span></span>
<span data-ttu-id="89294-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="89294-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89294-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="89294-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89294-121">Incorporación de Mindflash desde la galería</span><span class="sxs-lookup"><span data-stu-id="89294-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="89294-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="89294-123">Incorporación de Mindflash desde la galería</span><span class="sxs-lookup"><span data-stu-id="89294-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="89294-124">Para configurar la integración de Mindflash en Azure AD, será preciso que agregue Mindflash desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="89294-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89294-125">**Para agregar Mindflash desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="89294-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89294-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89294-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89294-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="89294-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89294-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="89294-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="89294-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89294-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="89294-133">En el cuadro de búsqueda, escriba **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="89294-133">In the search box, type **Mindflash**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="89294-135">En el panel de resultados, seleccione **Mindflash** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89294-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89294-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89294-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mindflash con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="89294-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89294-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Mindflash para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89294-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="89294-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Mindflash.</span><span class="sxs-lookup"><span data-stu-id="89294-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="89294-141">En Mindflash, para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="89294-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89294-142">Para configurar y probar el inicio de sesión único de Azure AD con Mindflash, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="89294-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89294-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="89294-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89294-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89294-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89294-145">**[Creación de un usuario de prueba de Mindflash](#creating-a-mindflash-test-user)**: para tener un homólogo de Britta Simon en Mindflash vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89294-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89294-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89294-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89294-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="89294-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89294-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89294-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Mindflash.</span><span class="sxs-lookup"><span data-stu-id="89294-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="89294-150">**Para configurar el inicio de sesión único de Azure AD con Mindflash, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="89294-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="89294-151">En Azure Portal, en la página de integración de la aplicación **Mindflash**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="89294-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="89294-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="89294-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="89294-155">En la sección **Dominio y direcciones URL de Mindflash**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="89294-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="89294-157">a.</span><span class="sxs-lookup"><span data-stu-id="89294-157">a.</span></span> <span data-ttu-id="89294-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.mindflash.com`.</span><span class="sxs-lookup"><span data-stu-id="89294-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="89294-159">b.</span><span class="sxs-lookup"><span data-stu-id="89294-159">b.</span></span> <span data-ttu-id="89294-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="89294-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89294-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="89294-161">These values are not real.</span></span> <span data-ttu-id="89294-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="89294-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="89294-163">Póngase en contacto con el [equipo de soporte técnico de Mindflash](https://www.mindflash.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="89294-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="89294-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="89294-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="89294-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="89294-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89294-168">Para configurar el inicio de sesión único en **Mindflash**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="89294-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="89294-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89294-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89294-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="89294-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89294-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89294-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89294-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="89294-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="89294-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="89294-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="89294-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89294-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89294-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89294-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="89294-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89294-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89294-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89294-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="89294-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89294-184">a.</span><span class="sxs-lookup"><span data-stu-id="89294-184">a.</span></span> <span data-ttu-id="89294-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89294-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89294-186">b.</span><span class="sxs-lookup"><span data-stu-id="89294-186">b.</span></span> <span data-ttu-id="89294-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89294-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89294-188">c.</span><span class="sxs-lookup"><span data-stu-id="89294-188">c.</span></span> <span data-ttu-id="89294-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="89294-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="89294-190">d.</span><span class="sxs-lookup"><span data-stu-id="89294-190">d.</span></span> <span data-ttu-id="89294-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="89294-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="89294-192">Creación de un usuario de prueba de Mindflash</span><span class="sxs-lookup"><span data-stu-id="89294-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="89294-193">Para permitir que los usuarios de Azure AD inicien sesión en Mindflash, deben aprovisionarse en Mindflash.</span><span class="sxs-lookup"><span data-stu-id="89294-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="89294-194">En el caso de Mindflash, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="89294-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="89294-195">Para aprovisionar cuentas de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="89294-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="89294-196">Inicie sesión como administrador en el sitio de la compañía de **Mindflash** .</span><span class="sxs-lookup"><span data-stu-id="89294-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="89294-197">Vaya a **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="89294-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="89294-198">![Administración de usuarios](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="89294-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="89294-199">Haga clic en **Agregar usuarios** y luego en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="89294-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="89294-200">En la sección **Agregar usuarios nuevos**, lleve a cabo los siguientes pasos para la cuenta de Azure AD válida que desea aprovisionar:</span><span class="sxs-lookup"><span data-stu-id="89294-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="89294-201">![Agregar nuevos usuarios](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Agregar nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="89294-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="89294-202">a.</span><span class="sxs-lookup"><span data-stu-id="89294-202">a.</span></span> <span data-ttu-id="89294-203">En el cuadro de texto **First name** (Nombre), escriba el **nombre** del usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="89294-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="89294-204">b.</span><span class="sxs-lookup"><span data-stu-id="89294-204">b.</span></span> <span data-ttu-id="89294-205">En el cuadro de texto **Last name** (Apellidos), escriba los **apellidos** del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="89294-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="89294-206">c.</span><span class="sxs-lookup"><span data-stu-id="89294-206">c.</span></span> <span data-ttu-id="89294-207">En el cuadro de texto **Email** (Correo electrónico), escriba la **dirección de correo electrónico** del usuario, en este caso **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="89294-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="89294-208">b.</span><span class="sxs-lookup"><span data-stu-id="89294-208">b.</span></span> <span data-ttu-id="89294-209">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="89294-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="89294-210">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Mindflash ofrecida por Mindflash para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="89294-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="89294-211">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89294-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="89294-212">En esta sección, concederá acceso a Britta Simon a Mindflash para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="89294-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="89294-214">**Para asignar el usuario Britta Simon a Mindflash, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="89294-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="89294-215">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="89294-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="89294-217">En la lista de aplicaciones, seleccione **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="89294-217">In the applications list, select **Mindflash**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="89294-219">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="89294-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="89294-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="89294-221">Click **Add** button.</span></span> <span data-ttu-id="89294-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="89294-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="89294-224">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="89294-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89294-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="89294-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89294-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="89294-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89294-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="89294-227">Testing single sign-on</span></span>

<span data-ttu-id="89294-228">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="89294-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="89294-229">Al hacer clic en el icono de Mindflash en el panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Mindflash.</span><span class="sxs-lookup"><span data-stu-id="89294-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="89294-230">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89294-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89294-231">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="89294-231">Additional resources</span></span>

* [<span data-ttu-id="89294-232">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89294-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89294-233">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89294-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

