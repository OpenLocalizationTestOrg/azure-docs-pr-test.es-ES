---
title: "Tutorial: Integración de Azure Active Directory con Land Gorilla Client | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Land Gorilla."
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="60efb-103">Tutorial: Integración de Azure Active Directory con Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="60efb-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="60efb-104">En este tutorial, obtendrá información sobre cómo integrar Land Gorilla Client con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60efb-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60efb-105">La integración de Land Gorilla Client con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="60efb-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60efb-106">Puede controlar en Azure AD quién tiene acceso a Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="60efb-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="60efb-107">Puede permitir que los usuarios inicien sesión automáticamente en Land Gorilla Client (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60efb-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="60efb-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="60efb-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60efb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="60efb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="60efb-110">Prerequisites</span></span>

<span data-ttu-id="60efb-111">Para configurar la integración de Azure AD con Land Gorilla Client, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="60efb-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="60efb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60efb-113">Una suscripción habilitada para el inicio de sesión único en Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="60efb-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="60efb-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="60efb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="60efb-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="60efb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60efb-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="60efb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="60efb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60efb-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="60efb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="60efb-118">Scenario description</span></span>
<span data-ttu-id="60efb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="60efb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60efb-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="60efb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60efb-121">Agregar Land Gorilla Client desde la galería</span><span class="sxs-lookup"><span data-stu-id="60efb-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="60efb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="60efb-123">Agregar Land Gorilla Client desde la galería</span><span class="sxs-lookup"><span data-stu-id="60efb-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="60efb-124">Para configurar la integración de Land Gorilla Client en Azure AD, deberá agregar Land Gorilla Client desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="60efb-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60efb-125">**Para agregar Land Gorilla Client desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="60efb-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60efb-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60efb-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60efb-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="60efb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60efb-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="60efb-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="60efb-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="60efb-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="60efb-133">En el cuadro de búsqueda, escriba **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="60efb-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="60efb-135">En el panel de resultados, seleccione **Land Gorilla Client** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60efb-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60efb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60efb-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Land Gorilla Client con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60efb-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60efb-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Land Gorilla Client para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60efb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="60efb-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="60efb-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="60efb-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="60efb-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="60efb-142">Para configurar y probar el inicio de sesión único de Azure AD con Land Gorilla Client, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="60efb-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60efb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="60efb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60efb-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con un grupo limitado.</span><span class="sxs-lookup"><span data-stu-id="60efb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="60efb-145">**[Creación de un usuario de prueba de Land Gorilla](#creating-a-land-gorilla-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60efb-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="60efb-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60efb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60efb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="60efb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60efb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60efb-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="60efb-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="60efb-150">**Para configurar el inicio de sesión único de Azure AD con Land Gorilla Client, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="60efb-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="60efb-151">En el Portal de administración de Azure, en la página de integración de la aplicación **Land Gorilla Client**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="60efb-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="60efb-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="60efb-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="60efb-155">En la sección **Dominio y direcciones URL de Land Gorilla Client**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="60efb-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="60efb-157">a.</span><span class="sxs-lookup"><span data-stu-id="60efb-157">a.</span></span> <span data-ttu-id="60efb-158">En el cuadro de texto **Identificador**, escriba un valor con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="60efb-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="60efb-159">b.</span><span class="sxs-lookup"><span data-stu-id="60efb-159">b.</span></span> <span data-ttu-id="60efb-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con uno de los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="60efb-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="60efb-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="60efb-161">Please note that these are not the real values.</span></span> <span data-ttu-id="60efb-162">Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="60efb-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="60efb-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="60efb-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="60efb-164">Póngase en contacto con el [equipo de soporte de Land Gorilla Client](https://www.landgorilla.com/support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="60efb-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="60efb-165">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="60efb-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="60efb-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="60efb-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="60efb-169">Para configurar el inicio de sesión único en el lado de su aplicación Land Gorilla, póngase en contacto con el [equipo de soporte de Land Gorilla Client](https://www.landgorilla.com/support/) para proporcionarles el archivo **XML de metadatos** descargado.</span><span class="sxs-lookup"><span data-stu-id="60efb-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60efb-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="60efb-171">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60efb-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="60efb-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="60efb-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60efb-174">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60efb-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60efb-176">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="60efb-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60efb-178">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="60efb-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60efb-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="60efb-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60efb-182">a.</span><span class="sxs-lookup"><span data-stu-id="60efb-182">a.</span></span> <span data-ttu-id="60efb-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60efb-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60efb-184">b.</span><span class="sxs-lookup"><span data-stu-id="60efb-184">b.</span></span> <span data-ttu-id="60efb-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60efb-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60efb-186">c.</span><span class="sxs-lookup"><span data-stu-id="60efb-186">c.</span></span> <span data-ttu-id="60efb-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="60efb-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60efb-188">d.</span><span class="sxs-lookup"><span data-stu-id="60efb-188">d.</span></span> <span data-ttu-id="60efb-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="60efb-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="60efb-190">Creación de un usuario de prueba de Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="60efb-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="60efb-191">Trabaje con el [equipo de soporte técnico de Land Gorilla](https://www.landgorilla.com/support/) para agregar los usuarios a la plataforma de Land Gorilla.</span><span class="sxs-lookup"><span data-stu-id="60efb-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60efb-192">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="60efb-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60efb-193">En esta sección, va a habilitar a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="60efb-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="60efb-195">**Para asignar a Britta Simon a Land Gorilla Client, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="60efb-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="60efb-196">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="60efb-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="60efb-198">En la lista de aplicaciones, seleccione **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="60efb-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="60efb-200">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="60efb-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="60efb-202">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="60efb-202">Click **Add** button.</span></span> <span data-ttu-id="60efb-203">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="60efb-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="60efb-205">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="60efb-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60efb-206">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="60efb-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60efb-207">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="60efb-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="60efb-208">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="60efb-208">Testing single sign-on</span></span>

<span data-ttu-id="60efb-209">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="60efb-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60efb-210">Al hacer clic en el icono de Land Gorilla Client en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="60efb-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="60efb-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="60efb-211">Additional resources</span></span>

* [<span data-ttu-id="60efb-212">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60efb-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60efb-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60efb-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
