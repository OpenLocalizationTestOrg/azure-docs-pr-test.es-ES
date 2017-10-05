---
title: "Tutorial: Integración de Azure Active Directory con Fuze | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="7a6c5-103">Tutorial: Integración de Azure Active Directory con Fuze</span><span class="sxs-lookup"><span data-stu-id="7a6c5-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="7a6c5-104">En este tutorial, obtendrá información sobre cómo integrar Fuze con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a6c5-105">Integrar Fuze con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a6c5-106">Puede controlar en Azure AD quién tiene acceso a Fuze</span><span class="sxs-lookup"><span data-stu-id="7a6c5-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="7a6c5-107">Puede permitir que los usuarios inicien sesión automáticamente en Fuze (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a6c5-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7a6c5-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a6c5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7a6c5-110">Prerequisites</span></span>

<span data-ttu-id="7a6c5-111">Para configurar la integración de Azure AD con Fuze, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="7a6c5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a6c5-113">Una suscripción habilitada para inicio de sesión único en Fuze</span><span class="sxs-lookup"><span data-stu-id="7a6c5-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="7a6c5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7a6c5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a6c5-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7a6c5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7a6c5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7a6c5-118">Scenario description</span></span>
<span data-ttu-id="7a6c5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a6c5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a6c5-121">Agregar Fuze desde la galería</span><span class="sxs-lookup"><span data-stu-id="7a6c5-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="7a6c5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="7a6c5-123">Agregar Fuze desde la galería</span><span class="sxs-lookup"><span data-stu-id="7a6c5-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="7a6c5-124">Para configurar la integración de Fuze en Azure AD, deberá agregar Fuze desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a6c5-125">**Para agregar Fuze desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7a6c5-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6c5-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a6c5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a6c5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7a6c5-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7a6c5-133">En el cuadro de búsqueda, escriba **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-133">In the search box, type **Fuze**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="7a6c5-135">En el panel de resultados, seleccione **Fuze** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a6c5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a6c5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Fuze con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7a6c5-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a6c5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Fuze para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="7a6c5-140">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Fuze.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="7a6c5-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Fuze.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="7a6c5-142">Para configurar y probar el inicio de sesión único de Azure AD con Fuze, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a6c5-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7a6c5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a6c5-145">**[Creación de un usuario de prueba de Fuze](#creating-a-fuze-test-user)**: para tener un homólogo de Britta Simon en Fuze que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7a6c5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a6c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a6c5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a6c5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Fuze.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="7a6c5-150">**Para configurar el inicio de sesión único de Azure AD con Fuze, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7a6c5-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6c5-151">En el Portal de administración de Azure, en la página de integración de la aplicación **Fuze**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7a6c5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="7a6c5-155">En la sección **Dominio y direcciones URL de Fuze**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="7a6c5-157">En el cuadro de texto **URL de inicio de sesión**, escriba la URL de inicio de sesión como: `https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="7a6c5-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="7a6c5-158">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7a6c5-158">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="7a6c5-160">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="7a6c5-162">Para configurar el inicio de sesión único en el lado de **Fuze**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="7a6c5-163">Ellos realizarán la configuración con el fin de que la conexión de SSO de SAML establecida correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a6c5-164">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a6c5-165">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7a6c5-167">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7a6c5-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6c5-168">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a6c5-170">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a6c5-172">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a6c5-174">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7a6c5-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a6c5-176">a.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-176">a.</span></span> <span data-ttu-id="7a6c5-177">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a6c5-178">b.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-178">b.</span></span> <span data-ttu-id="7a6c5-179">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a6c5-180">c.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-180">c.</span></span> <span data-ttu-id="7a6c5-181">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a6c5-182">d.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-182">d.</span></span> <span data-ttu-id="7a6c5-183">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="7a6c5-184">Creación de un usuario de prueba de Fuze</span><span class="sxs-lookup"><span data-stu-id="7a6c5-184">Creating a Fuze test user</span></span>

<span data-ttu-id="7a6c5-185">Fuze admite aprovisionamiento de usuarios Just-In-Time, por lo que los usuarios se crearán automáticamente al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="7a6c5-186">Para cualquier otra aclaración, póngase en contacto con el [equipo de soporte de Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a6c5-187">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6c5-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a6c5-188">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Fuze.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7a6c5-190">**Para asignar a Britta Simon a Fuze, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7a6c5-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6c5-191">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="7a6c5-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7a6c5-193">En la lista de aplicaciones, seleccione **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-193">In the applications list, select **Fuze**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="7a6c5-195">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-195">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7a6c5-197">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-197">Click **Add** button.</span></span> <span data-ttu-id="7a6c5-198">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7a6c5-200">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7a6c5-201">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a6c5-202">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="7a6c5-203">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7a6c5-203">Testing single sign-on</span></span>

<span data-ttu-id="7a6c5-204">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7a6c5-205">Al hacer clic en el icono de Fuze en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Fuze.</span><span class="sxs-lookup"><span data-stu-id="7a6c5-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7a6c5-206">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7a6c5-206">Additional resources</span></span>

* [<span data-ttu-id="7a6c5-207">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a6c5-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a6c5-208">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a6c5-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png