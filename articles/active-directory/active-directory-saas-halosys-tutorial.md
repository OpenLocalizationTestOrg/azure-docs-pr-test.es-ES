---
title: "Tutorial: Integración de Azure Active Directory con Halosys | Microsoft Docs"
description: "Aprenda a usar Halosys con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automático, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="3a056-103">Tutorial: Integración de Azure Active Directory con Halosys</span><span class="sxs-lookup"><span data-stu-id="3a056-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="3a056-104">En este tutorial, aprenderá a integrar Halosys con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a056-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a056-105">La integración de Halosys con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3a056-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a056-106">Puede controlar en Azure AD quién tiene acceso a Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="3a056-107">Puede permitir que los usuarios inicien sesión automáticamente en Halosys (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a056-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a056-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="3a056-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3a056-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a056-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a056-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3a056-110">Prerequisites</span></span>

<span data-ttu-id="3a056-111">Para configurar la integración de Azure AD con Halosys, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3a056-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="3a056-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a056-113">Una suscripción habilitada para el inicio de sesión único en Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="3a056-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3a056-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3a056-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3a056-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a056-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3a056-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3a056-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a056-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3a056-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3a056-118">Scenario description</span></span>
<span data-ttu-id="3a056-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3a056-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="3a056-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3a056-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a056-121">Adición de Halosys desde la galería</span><span class="sxs-lookup"><span data-stu-id="3a056-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="3a056-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="3a056-123">Adición de Halosys desde la galería</span><span class="sxs-lookup"><span data-stu-id="3a056-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="3a056-124">Para configurar la integración de Halosys en Azure AD, será preciso que agregue Halosys desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3a056-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a056-125">**Para agregar Halosys desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a056-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a056-126">En el **Portal de Azure clásico**, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a056-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="3a056-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="3a056-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3a056-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="3a056-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="3a056-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="3a056-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="3a056-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="3a056-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplicaciones][4]

6. <span data-ttu-id="3a056-135">En el cuadro de búsqueda, escriba **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="3a056-135">In the search box, type **Halosys**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="3a056-137">En el panel de resultados, seleccione **Halosys** y luego haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a056-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a056-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a056-140">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Halosys con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3a056-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a056-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Halosys para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a056-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="3a056-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="3a056-143">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="3a056-144">Para configurar y probar el inicio de sesión único de Azure AD con Halosys, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3a056-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a056-145">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3a056-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a056-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a056-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a056-147">**[Creación de un usuario de prueba de Halosys](#creating-a-halosys-test-user)**: para tener un homólogo de Britta Simon en Halosys que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a056-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3a056-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a056-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a056-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3a056-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a056-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a056-151">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal clásico y configurará el inicio de sesión único en la aplicación Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="3a056-152">**Para configurar el inicio de sesión único de Azure AD con Halosys, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3a056-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="3a056-153">En el portal clásico, en la página de integración de aplicaciones de **Halosys**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3a056-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="3a056-155">En la página **How would you like users to sign on to HPE SaaS** (¿Cómo desea que los usuarios inicien sesión en HPE SaaS?), seleccione **Inicio de sesión único de Azure AD** y después haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a056-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="3a056-157">En la página de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3a056-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="3a056-159">a.</span><span class="sxs-lookup"><span data-stu-id="3a056-159">a.</span></span> <span data-ttu-id="3a056-160">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL que usan los usuarios para iniciar sesión en su aplicación de Halosys con el siguiente patrón: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="3a056-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="3a056-161">b. En el cuadro de texto **Identifier URL** (URL del identificador), escriba la dirección URL con el siguiente patrón: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="3a056-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="3a056-162">En la página **Configurar inicio de sesión único en Halosys**, haga clic en **Descargar metadatos** y luego guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3a056-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="3a056-164">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el equipo de soporte técnico de Halosys y proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a056-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="3a056-165">• El **archivo de metadatos** descargado</span><span class="sxs-lookup"><span data-stu-id="3a056-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="3a056-166">• La **dirección URL de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="3a056-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="3a056-167">En el portal clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a056-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="3a056-169">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="3a056-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Inicio de sesión único de Azure AD ][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a056-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a056-172">En esta sección, creará un usuario de prueba llamado Britta Simon en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="3a056-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Creación de un usuario de Azure AD][20]

<span data-ttu-id="3a056-174">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3a056-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a056-175">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a056-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3a056-177">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="3a056-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3a056-178">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3a056-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a056-180">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3a056-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3a056-182">En el **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos siguientes: ![crear un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="3a056-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="3a056-183">a.</span><span class="sxs-lookup"><span data-stu-id="3a056-183">a.</span></span> <span data-ttu-id="3a056-184">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="3a056-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="3a056-185">b.</span><span class="sxs-lookup"><span data-stu-id="3a056-185">b.</span></span> <span data-ttu-id="3a056-186">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a056-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a056-187">c.</span><span class="sxs-lookup"><span data-stu-id="3a056-187">c.</span></span> <span data-ttu-id="3a056-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a056-188">Click **Next**.</span></span>

6.  <span data-ttu-id="3a056-189">En el cuadro de diálogo **Perfil de usuario**, siga estos pasos: ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="3a056-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="3a056-190">a.</span><span class="sxs-lookup"><span data-stu-id="3a056-190">a.</span></span> <span data-ttu-id="3a056-191">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3a056-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="3a056-192">b.</span><span class="sxs-lookup"><span data-stu-id="3a056-192">b.</span></span> <span data-ttu-id="3a056-193">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a056-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="3a056-194">c.</span><span class="sxs-lookup"><span data-stu-id="3a056-194">c.</span></span> <span data-ttu-id="3a056-195">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a056-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3a056-196">d.</span><span class="sxs-lookup"><span data-stu-id="3a056-196">d.</span></span> <span data-ttu-id="3a056-197">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="3a056-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="3a056-198">e.</span><span class="sxs-lookup"><span data-stu-id="3a056-198">e.</span></span> <span data-ttu-id="3a056-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a056-199">Click **Next**.</span></span>

7. <span data-ttu-id="3a056-200">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a056-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3a056-202">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3a056-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="3a056-204">a.</span><span class="sxs-lookup"><span data-stu-id="3a056-204">a.</span></span> <span data-ttu-id="3a056-205">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3a056-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="3a056-206">b.</span><span class="sxs-lookup"><span data-stu-id="3a056-206">b.</span></span> <span data-ttu-id="3a056-207">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="3a056-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="3a056-208">Creación de un usuario de prueba de Halosys</span><span class="sxs-lookup"><span data-stu-id="3a056-208">Creating a Halosys test user</span></span>

<span data-ttu-id="3a056-209">En esta sección, creará un usuario llamado Britta Simon en Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="3a056-210">Trabaje con el equipo de soporte técnico de Halosys para agregar los usuarios a la plataforma de Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a056-211">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a056-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a056-212">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3a056-214">**Para asignar a Britta Simon a Halosys, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a056-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="3a056-215">En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="3a056-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3a056-217">En la lista de aplicaciones, seleccione **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="3a056-217">In the applications list, select **Halosys**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="3a056-219">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3a056-219">In the menu on the top, click **Users**.</span></span>

    ![Asignar usuario][203]

4. <span data-ttu-id="3a056-221">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a056-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3a056-222">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="3a056-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="3a056-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3a056-224">Testing single sign-on</span></span>

<span data-ttu-id="3a056-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3a056-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a056-226">Al hacer clic en el icono de Halosys en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Halosys.</span><span class="sxs-lookup"><span data-stu-id="3a056-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3a056-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3a056-227">Additional resources</span></span>

* [<span data-ttu-id="3a056-228">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a056-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a056-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a056-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
