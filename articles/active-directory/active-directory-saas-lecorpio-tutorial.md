---
title: "Tutorial: Integración de Azure Active Directory con Lecorpio | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="049e0-103">Tutorial: Integración de Azure Active Directory con Lecorpio</span><span class="sxs-lookup"><span data-stu-id="049e0-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="049e0-104">En este tutorial, aprenderá a integrar Lecorpio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="049e0-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="049e0-105">La integración de Lecorpio con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="049e0-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="049e0-106">Puede controlar en Azure AD quién tiene acceso a Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="049e0-107">Puede permitir que los usuarios inicien sesión automáticamente en Lecorpio (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="049e0-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="049e0-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="049e0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="049e0-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="049e0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="049e0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="049e0-110">Prerequisites</span></span>

<span data-ttu-id="049e0-111">Para configurar la integración de Azure AD con Lecorpio, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="049e0-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="049e0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="049e0-113">Una suscripción habilitada para inicio de sesión único en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="049e0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="049e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="049e0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="049e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="049e0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="049e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="049e0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="049e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="049e0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="049e0-118">Scenario description</span></span>
<span data-ttu-id="049e0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="049e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="049e0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="049e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="049e0-121">Adición de Lecorpio desde la galería</span><span class="sxs-lookup"><span data-stu-id="049e0-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="049e0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="049e0-123">Adición de Lecorpio desde la galería</span><span class="sxs-lookup"><span data-stu-id="049e0-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="049e0-124">Para configurar la integración de Lecorpio en Azure AD, deberá agregar Lecorpio desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="049e0-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="049e0-125">**Para agregar Lecorpio desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="049e0-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="049e0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="049e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="049e0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="049e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="049e0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="049e0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="049e0-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049e0-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="049e0-133">En el cuadro de búsqueda, escriba **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="049e0-133">In the search box, type **Lecorpio**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="049e0-135">En el panel de resultados, seleccione **Lecorpio** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="049e0-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="049e0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="049e0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lecorpio con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="049e0-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="049e0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Lecorpio para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="049e0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="049e0-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="049e0-141">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como el valor de **nombre de usuario** en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="049e0-142">Para configurar y probar el inicio de sesión único de Azure AD con Lecorpio, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="049e0-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="049e0-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="049e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="049e0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="049e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="049e0-145">**[Creación de un usuario de prueba de Lecorpio](#creating-a-lecorpio-test-user)**: para tener un homólogo de Britta Simon en Lecorpio que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="049e0-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="049e0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="049e0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="049e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="049e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="049e0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="049e0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal de Azure y configurará el inicio de sesión único en la aplicación Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="049e0-150">**Para configurar el inicio de sesión único de Azure AD con Lecorpio, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="049e0-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="049e0-151">En el portal de Azure, en la página de integración de la aplicación **Lecorpio**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="049e0-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="049e0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="049e0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="049e0-155">En la sección **Dominio y direcciones URL de Lecorpio**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="049e0-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="049e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="049e0-157">a.</span></span> <span data-ttu-id="049e0-158">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="049e0-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="049e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="049e0-159">b.</span></span> <span data-ttu-id="049e0-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="049e0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="049e0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="049e0-161">These values are not the real.</span></span> <span data-ttu-id="049e0-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="049e0-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="049e0-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="049e0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="049e0-164">Póngase en contacto con el [equipo de soporte de cliente de Lecorpio](mailto:info@lecorpio.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="049e0-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="049e0-165">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="049e0-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="049e0-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="049e0-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="049e0-169">Para configurar el inicio de sesión único en el lado de **Lecorpio**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="049e0-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="049e0-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="049e0-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="049e0-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="049e0-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="049e0-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="049e0-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="049e0-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="049e0-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="049e0-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="049e0-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="049e0-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="049e0-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="049e0-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="049e0-179">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="049e0-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="049e0-181">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="049e0-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="049e0-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="049e0-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="049e0-185">a.</span><span class="sxs-lookup"><span data-stu-id="049e0-185">a.</span></span> <span data-ttu-id="049e0-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="049e0-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="049e0-187">b.</span><span class="sxs-lookup"><span data-stu-id="049e0-187">b.</span></span> <span data-ttu-id="049e0-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="049e0-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="049e0-189">c.</span><span class="sxs-lookup"><span data-stu-id="049e0-189">c.</span></span> <span data-ttu-id="049e0-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="049e0-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="049e0-191">d.</span><span class="sxs-lookup"><span data-stu-id="049e0-191">d.</span></span> <span data-ttu-id="049e0-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="049e0-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="049e0-193">Creación de un usuario de prueba de Lecorpio</span><span class="sxs-lookup"><span data-stu-id="049e0-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="049e0-194">En esta sección, creará un usuario llamado Britta Simon en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="049e0-195">Póngase en contacto con el [equipo de soporte técnico del cliente de Lecorpio](mailto:info@lecorpio.com) para agregar los usuarios en la aplicación Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="049e0-196">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="049e0-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="049e0-197">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="049e0-199">**Para asignar a Britta Simon a Lecorpio, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="049e0-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="049e0-200">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="049e0-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="049e0-202">En la lista de aplicaciones, seleccione **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="049e0-202">In the applications list, select **Lecorpio**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="049e0-204">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="049e0-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="049e0-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="049e0-206">Click **Add** button.</span></span> <span data-ttu-id="049e0-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="049e0-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="049e0-209">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="049e0-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="049e0-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="049e0-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="049e0-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="049e0-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="049e0-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="049e0-212">Testing single sign-on</span></span>

<span data-ttu-id="049e0-213">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="049e0-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="049e0-214">Al hacer clic en el icono de Lecorpio en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="049e0-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="049e0-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="049e0-215">Additional resources</span></span>

* [<span data-ttu-id="049e0-216">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="049e0-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="049e0-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="049e0-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

