---
title: "Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Splunk Enterprise y Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="ed85f-103">Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="ed85f-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="ed85f-104">En este tutorial, aprenderá a integrar Splunk Enterprise y Splunk Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed85f-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed85f-105">La integración de Splunk Enterprise y Splunk Cloud con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ed85f-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed85f-106">Puede controlar en Azure AD quién tiene acceso a Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="ed85f-107">Puede permitir que los usuarios inicien sesión automáticamente en Splunk Enterprise y Splunk Cloud mediante inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed85f-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed85f-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="ed85f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ed85f-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed85f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed85f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed85f-110">Prerequisites</span></span>

<span data-ttu-id="ed85f-111">Para configurar la integración de Azure AD con Splunk Enterprise y Splunk Cloud, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ed85f-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="ed85f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed85f-113">Una suscripción habilitada para el SSO en Splunk Enterprise o Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="ed85f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ed85f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="ed85f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ed85f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed85f-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ed85f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ed85f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed85f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ed85f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ed85f-118">Scenario description</span></span>
<span data-ttu-id="ed85f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ed85f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="ed85f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ed85f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed85f-121">Adición de Splunk Enterprise y Splunk Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="ed85f-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="ed85f-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="ed85f-123">Adición de Splunk Enterprise y Splunk Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="ed85f-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="ed85f-124">Para configurar la integración de Splunk Enterprise y Splunk Cloud en Azure AD, deberá agregar Splunk Enterprise y Splunk Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ed85f-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed85f-125">**Para agregar Splunk Enterprise y Splunk Cloud desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ed85f-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed85f-126">En el **Portal de Azure clásico**, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="ed85f-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="ed85f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ed85f-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="ed85f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="ed85f-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="ed85f-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="ed85f-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplicaciones][4]

6. <span data-ttu-id="ed85f-135">En el cuadro de búsqueda, escriba **Splunk Enterprise o Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="ed85f-137">En el panel de resultados, seleccione **Splunk Enterprise y Splunk Cloud** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed85f-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ed85f-139">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ed85f-140">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ed85f-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed85f-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Splunk Enterprise y Splunk Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed85f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="ed85f-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="ed85f-143">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor de **nombre de usuario** en Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="ed85f-144">Para configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ed85f-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed85f-145">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ed85f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed85f-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed85f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed85f-147">**[Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**: para tener un homólogo de Britta Simon en Splunk Enterprise y Splunk Cloud que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed85f-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ed85f-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed85f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed85f-149">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ed85f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ed85f-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ed85f-151">En esta sección, habilitará el SSO de Azure AD en el portal clásico y lo configurará en la aplicación Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="ed85f-152">**Para configurar el inicio de sesión único en Azure AD con Splunk Enterprise y Splunk Cloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed85f-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ed85f-153">En el portal clásico, en la página de integración de aplicaciones de **Splunk Enterprise y Splunk Cloud**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="ed85f-155">En la página **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** (¿Cómo desea que los usuarios inicien sesión en Splunk Enterprise y Splunk Cloud?), seleccione **Inicio de sesión único de Azure AD** y después haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="ed85f-157">En la página de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ed85f-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="ed85f-159">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL que los usuarios usan para iniciar sesión en su aplicación Splunk Enterprise y Splunk Cloud con el siguiente patrón: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="ed85f-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="ed85f-160">En el cuadro de texto **Identificador**, escriba la dirección URL de su instancia de Splunk Server:</span><span class="sxs-lookup"><span data-stu-id="ed85f-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="ed85f-161">En el cuadro de texto **URL de respuesta**, escriba la dirección URL con el siguiente patrón: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="ed85f-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="ed85f-162">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="ed85f-163">En la página **Configurar inicio de sesión único en Splunk Enterprise y Splunk Cloud**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ed85f-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="ed85f-165">Haga clic en **Descargar metadatos**y luego guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ed85f-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="ed85f-166">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-166">Click **Next**.</span></span>

5. <span data-ttu-id="ed85f-167">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el equipo de soporte técnico de Splunk Enterprise y Splunk Cloud y proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="ed85f-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="ed85f-168">Los **metadatos de federación** descargados.</span><span class="sxs-lookup"><span data-stu-id="ed85f-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="ed85f-169">En el portal clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="ed85f-171">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ed85f-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-173">Create an Azure AD test user</span></span>
<span data-ttu-id="ed85f-174">En esta sección, creará un usuario de prueba llamado Britta Simon en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="ed85f-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="ed85f-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ed85f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed85f-177">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="ed85f-179">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="ed85f-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ed85f-180">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed85f-182">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="ed85f-184">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ed85f-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="ed85f-186">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="ed85f-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="ed85f-187">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ed85f-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-188">Click **Next**.</span></span>

6.  <span data-ttu-id="ed85f-189">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ed85f-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="ed85f-191">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="ed85f-192">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="ed85f-193">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ed85f-194">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ed85f-195">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-195">Click **Next**.</span></span>

7. <span data-ttu-id="ed85f-196">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="ed85f-198">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ed85f-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="ed85f-200">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="ed85f-201">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="ed85f-202">Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="ed85f-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="ed85f-203">En esta sección, creará un usuario llamado Britta Simon en Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="ed85f-204">Trabaje con el equipo de soporte técnico de Splunk Enterprise y Splunk Cloud para agregar los usuarios a la plataforma de Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ed85f-205">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed85f-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="ed85f-206">En esta sección, permitirá que Britta Simon use el SSO de Azure concediéndole acceso a Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ed85f-208">**Para asignar Britta Simon a Splunk Enterprise y Splunk Cloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed85f-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ed85f-209">En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="ed85f-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ed85f-211">En la lista de aplicaciones, seleccione **Splunk Enterprise y Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="ed85f-213">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-213">In the menu on the top, click **Users**.</span></span>

    ![Asignar usuario][203]

4. <span data-ttu-id="ed85f-215">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="ed85f-216">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="ed85f-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ed85f-218">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ed85f-218">Test single sign-on</span></span>

<span data-ttu-id="ed85f-219">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ed85f-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="ed85f-220">Al hacer clic en el icono de Splunk Enterprise y Splunk Cloud en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="ed85f-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ed85f-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ed85f-221">Additional resources</span></span>

* [<span data-ttu-id="ed85f-222">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed85f-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed85f-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed85f-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
