---
title: "Tutorial: Integración de Azure Active Directory con SciQuest Spend Director | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SciQuest Spend Director."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="f8aca-103">Tutorial: Integración de Azure Active Directory con SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="f8aca-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="f8aca-104">El objetivo de este tutorial es mostrar cómo integrar SciQuest Spend Director con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8aca-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="f8aca-105">La integración de SciQuest Spend Director con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f8aca-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="f8aca-106">Puede controlar en Azure AD quién tiene acceso a SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="f8aca-107">Puede permitir que los usuarios inicien sesión automáticamente en SciQuest Spend Director (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8aca-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f8aca-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="f8aca-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f8aca-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8aca-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8aca-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f8aca-110">Prerequisites</span></span>
<span data-ttu-id="f8aca-111">Para configurar la integración de Azure AD con SciQuest Spend Director, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f8aca-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="f8aca-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f8aca-113">Una suscripción de SciQuest Spend Director habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f8aca-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8aca-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f8aca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f8aca-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f8aca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f8aca-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f8aca-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f8aca-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8aca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="f8aca-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f8aca-118">Scenario Description</span></span>
<span data-ttu-id="f8aca-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f8aca-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="f8aca-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f8aca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8aca-121">Agregar SciQuest Spend Director desde la galería</span><span class="sxs-lookup"><span data-stu-id="f8aca-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="f8aca-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="f8aca-123">Agregar SciQuest Spend Director desde la galería</span><span class="sxs-lookup"><span data-stu-id="f8aca-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="f8aca-124">Para configurar la integración de SciQuest Spend Director en Azure AD, deberá agregar SciQuest Spend Director desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f8aca-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f8aca-125">**Para agregar SciQuest Spend Director desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f8aca-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f8aca-126">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="f8aca-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="f8aca-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f8aca-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="f8aca-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="f8aca-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="f8aca-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="f8aca-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="f8aca-135">En el cuadro de búsqueda, escriba **SciQuest Spend Director**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="f8aca-137">En el panel de resultados, seleccione **SciQuest Spend Director** y, después, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f8aca-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![Aplicaciones][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8aca-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8aca-140">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con SciQuest Spend Director según un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f8aca-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8aca-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SciQuest Spend Director para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8aca-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="f8aca-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="f8aca-143">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="f8aca-144">Para configurar y probar el inicio de sesión único de Azure AD con SciQuest Spend Director, debe completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f8aca-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f8aca-145">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f8aca-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f8aca-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8aca-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8aca-147">**[Creación de un usuario de prueba de SciQuest Spend Director](#creating-a-halogen-software-test-user)** : para tener un homólogo de Britta Simon en SciQuest Spend Director que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8aca-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f8aca-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8aca-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8aca-149">**[Prueba del inicio de sesión único](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f8aca-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="f8aca-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="f8aca-151">El objetivo de esta sección es habilitar el inicio de sesión único de Azure AD en el Portal de Azure clásico y configurar el inicio de sesión único en la aplicación de SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="f8aca-152">**Para configurar el inicio de sesión único de Azure AD con SciQuest Spend Director, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f8aca-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="f8aca-153">En el Portal de Azure clásico, en la página de integración de aplicaciones de **SciQuest Spend Director**, haga clic en **Configurar inicio de sesión único** para abrir el diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][8]

2. <span data-ttu-id="f8aca-155">En la página **¿Cómo desea que los usuarios inicien sesión en SciQuest Spend Director?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]

3. <span data-ttu-id="f8aca-157">En la página de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8aca-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configurar las opciones de la aplicación][10]
   
     <span data-ttu-id="f8aca-159">a.</span><span class="sxs-lookup"><span data-stu-id="f8aca-159">a.</span></span> <span data-ttu-id="f8aca-160">En el cuadro de texto **Dirección URL de inicio de sesión**, escriba la dirección URL que utilizan los usuarios para iniciar sesión en la aplicación de SciQuest Spend Director con el patrón siguiente: *https://.*sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="f8aca-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="f8aca-161">b.</span><span class="sxs-lookup"><span data-stu-id="f8aca-161">b.</span></span> <span data-ttu-id="f8aca-162">En el cuadro de texto **URL de respuesta**, escriba el mismo valor que ha escrito en el cuadro de texto **Dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="f8aca-163">c.</span><span class="sxs-lookup"><span data-stu-id="f8aca-163">c.</span></span> <span data-ttu-id="f8aca-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-164">Click **Next**.</span></span>

4. <span data-ttu-id="f8aca-165">En la página **Configurar inicio de sesión único en SciQuest Spend Director**, haga clic en **Descargar metadatos** y, después, guarde el archivo de metadatos de forma local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f8aca-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Qué es Azure AD Connect][11]

5. <span data-ttu-id="f8aca-167">Póngase en contacto con el soporte técnico de SciQuest para habilitar este método de autenticación mediante los datos descargados anteriores.</span><span class="sxs-lookup"><span data-stu-id="f8aca-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="f8aca-168">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![Qué es Azure AD Connect][15]

7. <span data-ttu-id="f8aca-170">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8aca-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8aca-172">El objetivo de esta sección es crear un usuario de prueba en el Portal de Azure clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8aca-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="f8aca-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f8aca-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f8aca-174">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Qué es Azure AD Connect][100] 

2. <span data-ttu-id="f8aca-176">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="f8aca-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f8aca-177">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][101] 

4. <span data-ttu-id="f8aca-179">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Qué es Azure AD Connect][102] 

5. <span data-ttu-id="f8aca-181">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8aca-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Qué es Azure AD Connect][103] 
   
    <span data-ttu-id="f8aca-183">a.</span><span class="sxs-lookup"><span data-stu-id="f8aca-183">a.</span></span> <span data-ttu-id="f8aca-184">En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="f8aca-185">b.</span><span class="sxs-lookup"><span data-stu-id="f8aca-185">b.</span></span> <span data-ttu-id="f8aca-186">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f8aca-187">c.</span><span class="sxs-lookup"><span data-stu-id="f8aca-187">c.</span></span> <span data-ttu-id="f8aca-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-188">Click **Next**.</span></span>

6. <span data-ttu-id="f8aca-189">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8aca-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Qué es Azure AD Connect][104] 
   
    <span data-ttu-id="f8aca-191">a.</span><span class="sxs-lookup"><span data-stu-id="f8aca-191">a.</span></span> <span data-ttu-id="f8aca-192">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="f8aca-193">b.</span><span class="sxs-lookup"><span data-stu-id="f8aca-193">b.</span></span> <span data-ttu-id="f8aca-194">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f8aca-195">c.</span><span class="sxs-lookup"><span data-stu-id="f8aca-195">c.</span></span> <span data-ttu-id="f8aca-196">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f8aca-197">d.</span><span class="sxs-lookup"><span data-stu-id="f8aca-197">d.</span></span> <span data-ttu-id="f8aca-198">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f8aca-199">e.</span><span class="sxs-lookup"><span data-stu-id="f8aca-199">e.</span></span> <span data-ttu-id="f8aca-200">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-200">Click **Next**.</span></span>

7. <span data-ttu-id="f8aca-201">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Qué es Azure AD Connect][105]  

8. <span data-ttu-id="f8aca-203">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8aca-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Qué es Azure AD Connect][106]   
   
    <span data-ttu-id="f8aca-205">a.</span><span class="sxs-lookup"><span data-stu-id="f8aca-205">a.</span></span> <span data-ttu-id="f8aca-206">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="f8aca-207">b.</span><span class="sxs-lookup"><span data-stu-id="f8aca-207">b.</span></span> <span data-ttu-id="f8aca-208">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="f8aca-209">Creación de un usuario de prueba de SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="f8aca-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="f8aca-210">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="f8aca-211">Deberá ponerse en contacto con el equipo de soporte técnico de SciQuest Spend Director y proporcionarles los detalles acerca de la cuenta de prueba que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="f8aca-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="f8aca-212">Como alternativa, también puede aprovechar el aprovisionamiento Just-In-Time, una característica de inicio de sesión único que es compatible con SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="f8aca-213">Si el aprovisionamiento Just-In-Time está habilitado, los usuarios se crean automáticamente en SciQuest Spend Director durante un intento de inicio de sesión único, si no existen.</span><span class="sxs-lookup"><span data-stu-id="f8aca-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="f8aca-214">Esta característica elimina la necesidad de crear manualmente usuarios homólogos de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8aca-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="f8aca-215">Para habilitar el aprovisionamiento Just-In-Timed, deberá ponerse en contacto con el equipo de soporte técnico de SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f8aca-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8aca-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="f8aca-217">El objetivo de esta sección es permitir que Britta Simon utilice el inicio de sesión único de Azure concediéndole acceso a SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![Qué es Azure AD Connect][200]

<span data-ttu-id="f8aca-219">**Para asignar a Britta Simon a SciQuest Spend Director, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f8aca-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="f8aca-220">En el Portal de Azure clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="f8aca-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Qué es Azure AD Connect][201]

2. <span data-ttu-id="f8aca-222">En la lista de aplicaciones, seleccione **SciQuest Spend Director**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Qué es Azure AD Connect][202]

3. <span data-ttu-id="f8aca-224">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-224">In the menu on the top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][203]

4. <span data-ttu-id="f8aca-226">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![Qué es Azure AD Connect][204]

5. <span data-ttu-id="f8aca-228">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="f8aca-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Qué es Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f8aca-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f8aca-230">Testing Single Sign-On</span></span>
<span data-ttu-id="f8aca-231">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f8aca-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f8aca-232">Al hacer clic en el icono de SciQuest Spend Director en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="f8aca-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8aca-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f8aca-233">Additional Resources</span></span>
* [<span data-ttu-id="f8aca-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8aca-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8aca-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8aca-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

