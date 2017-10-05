---
title: "Tutorial: integración de Azure Active Directory con Soonr Workplace | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Soonr Workplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="c6eb1-103">Tutorial: integración de Azure Active Directory con Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c6eb1-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="c6eb1-104">El objetivo de este tutorial es mostrar cómo integrar Soonr Workplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="c6eb1-105">Integrar Soonr Workplace con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6eb1-106">Puede controlar en Azure AD quién tiene acceso a Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="c6eb1-107">Puede permitir que los usuarios inicien sesión automáticamente en Soonr Workplace (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6eb1-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c6eb1-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6eb1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6eb1-110">Prerequisites</span></span>

<span data-ttu-id="c6eb1-111">Para configurar la integración de Azure AD con Soonr Workplace, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="c6eb1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6eb1-113">Una suscripción habilitada para inicio de sesión único en Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c6eb1-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="c6eb1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c6eb1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6eb1-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c6eb1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c6eb1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c6eb1-118">Scenario description</span></span>
<span data-ttu-id="c6eb1-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="c6eb1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6eb1-121">Incorporación de Soonr Workplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="c6eb1-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="c6eb1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="c6eb1-123">Incorporación de Soonr Workplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="c6eb1-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="c6eb1-124">Para configurar la integración de Soonr Workplace en Azure AD, deberá agregar Soonr Workplace desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6eb1-125">**Para agregar Soonr Workplace desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6eb1-126">En el **Portal de Azure clásico**, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6eb1-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c6eb1-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="c6eb1-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="c6eb1-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Aplicaciones][4]

6. <span data-ttu-id="c6eb1-135">En el cuadro de búsqueda, escriba **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="c6eb1-137">En el panel de resultados, seleccione **Soonr Workplace** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6eb1-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6eb1-140">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con Soonr Workplace con una usuaria de prueba llamada "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c6eb1-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6eb1-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Soonr Workplace para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="c6eb1-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="c6eb1-143">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="c6eb1-144">Para configurar y probar el inicio de sesión único de Azure AD con Soonr Workplace, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6eb1-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6eb1-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6eb1-147">**[Creación de un usuario de prueba de Soonr Workplace](#creating-a-soonr-workplace-test-user)** : para tener un homólogo de Britta Simon en Soonr Workplace que esté vinculado a la representación de esta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c6eb1-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6eb1-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6eb1-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6eb1-151">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal clásico y configurará el inicio de sesión único en la aplicación Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="c6eb1-152">**Para configurar el inicio de sesión único de Azure AD con Soonr Workplace, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c6eb1-153">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Soonr Workplace**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="c6eb1-155">En la página **¿Cómo desea que los usuarios inicien sesión en Soonr Workplace?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="c6eb1-157">En la página del cuadro de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="c6eb1-159">a.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-159">a.</span></span> <span data-ttu-id="c6eb1-160">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="c6eb1-161">b.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-161">b.</span></span> <span data-ttu-id="c6eb1-162">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6eb1-163">Tenga en cuenta que este no es el valor real.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-163">Please note that this is not the real value.</span></span> <span data-ttu-id="c6eb1-164">Tiene que actualizar este valor con la URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="c6eb1-165">Póngase en contacto con el equipo de soporte técnico de Soonr Workplace para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="c6eb1-166">En la página **Configuración de inicio de sesión único** de Soonr Workplace, haga clic en **Descargar metadatos** y luego guarde el archivo en el equipo:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="c6eb1-168">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el equipo de soporte técnico de Soonr Workplace y proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="c6eb1-169">•  El archivo de **metadatos** descargado</span><span class="sxs-lookup"><span data-stu-id="c6eb1-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="c6eb1-170">• La **dirección URL del emisor**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="c6eb1-171">La **dirección URL de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="c6eb1-172">La **dirección URL del servicio de cierre de sesión único**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="c6eb1-173">Esta aplicación se ha sustituido por <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> y puede consultar <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">este</a> tutorial para configurar la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="c6eb1-174">En el Portal de Azure clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="c6eb1-176">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Inicio de sesión único de Azure AD ][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6eb1-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6eb1-179">El objetivo de esta sección es crear un usuario de prueba en el Portal de Azure clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="c6eb1-181">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6eb1-182">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="c6eb1-184">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c6eb1-185">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6eb1-187">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="c6eb1-189">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="c6eb1-191">a.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-191">a.</span></span> <span data-ttu-id="c6eb1-192">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="c6eb1-193">b.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-193">b.</span></span> <span data-ttu-id="c6eb1-194">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6eb1-195">c.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-195">c.</span></span> <span data-ttu-id="c6eb1-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-196">Click **Next**.</span></span>

6.  <span data-ttu-id="c6eb1-197">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="c6eb1-199">a.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-199">a.</span></span> <span data-ttu-id="c6eb1-200">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="c6eb1-201">b.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-201">b.</span></span> <span data-ttu-id="c6eb1-202">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="c6eb1-203">c.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-203">c.</span></span> <span data-ttu-id="c6eb1-204">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c6eb1-205">d.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-205">d.</span></span> <span data-ttu-id="c6eb1-206">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="c6eb1-207">e.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-207">e.</span></span> <span data-ttu-id="c6eb1-208">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-208">Click **Next**.</span></span>

7. <span data-ttu-id="c6eb1-209">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="c6eb1-211">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="c6eb1-213">a.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-213">a.</span></span> <span data-ttu-id="c6eb1-214">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="c6eb1-215">b.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-215">b.</span></span> <span data-ttu-id="c6eb1-216">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="c6eb1-217">Creación de un usuario de prueba de Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c6eb1-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="c6eb1-218">El objetivo de esta sección es crear una usuaria llamada Britta Simon en Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="c6eb1-219">Trabaje con el equipo de soporte técnico de Soonr Workplace para crear un usuario en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="c6eb1-220">Puede enviar la incidencia de soporte técnico a Soonr desde <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aquí</a>.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c6eb1-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6eb1-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c6eb1-222">El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure, para lo cual se le concederá acceso a Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c6eb1-224">**Para asignar la usuaria Britta Simon a Soonr Workplace, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6eb1-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c6eb1-225">En el Portal de Azure clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en la opción **Aplicaciones** del menú superior.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c6eb1-227">En la lista de aplicaciones, seleccione **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="c6eb1-229">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-229">In the menu on the top, click **Users**.</span></span>

    ![Asignar usuario][203] 

1. <span data-ttu-id="c6eb1-231">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="c6eb1-232">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="c6eb1-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c6eb1-234">Testing single sign-on</span></span>

<span data-ttu-id="c6eb1-235">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="c6eb1-236">Al hacer clic en el icono de Soonr Workplace en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c6eb1-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c6eb1-237">Additional resources</span></span>

* [<span data-ttu-id="c6eb1-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6eb1-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6eb1-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6eb1-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
