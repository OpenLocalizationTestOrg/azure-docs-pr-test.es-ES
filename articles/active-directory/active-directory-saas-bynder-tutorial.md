---
title: "Tutorial: Integración de Azure Active Directory con Bynder | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="d0b28-103">Tutorial: Integración de Azure Active Directory con Bynder</span><span class="sxs-lookup"><span data-stu-id="d0b28-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="d0b28-104">El objetivo de este tutorial es mostrar cómo integrar Bynder con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0b28-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0b28-105">Integrar Bynder con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d0b28-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d0b28-106">Puede controlar en Azure AD quién tiene acceso a Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="d0b28-107">Puede permitir que los usuarios inicien sesión automáticamente en Bynder (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0b28-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d0b28-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="d0b28-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d0b28-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0b28-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0b28-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d0b28-110">Prerequisites</span></span>
<span data-ttu-id="d0b28-111">Para configurar la integración de Azure AD con Bynder, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d0b28-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="d0b28-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d0b28-113">Una suscripción habilitada para el inicio de sesión único en Bynder</span><span class="sxs-lookup"><span data-stu-id="d0b28-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d0b28-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d0b28-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d0b28-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d0b28-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d0b28-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d0b28-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d0b28-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0b28-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0b28-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d0b28-118">Scenario description</span></span>
<span data-ttu-id="d0b28-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Microsoft Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d0b28-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="d0b28-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d0b28-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0b28-121">Adición de Bynder desde la galería</span><span class="sxs-lookup"><span data-stu-id="d0b28-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="d0b28-122">Configuración y prueba del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="d0b28-123">Adición de Bynder desde la galería</span><span class="sxs-lookup"><span data-stu-id="d0b28-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="d0b28-124">Para configurar la integración de Bynder en Azure AD, deberá agregar Bynder desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d0b28-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0b28-125">**Para agregar Bynder desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d0b28-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0b28-126">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d0b28-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="d0b28-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d0b28-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="d0b28-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d0b28-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="d0b28-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="d0b28-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="d0b28-135">En el cuadro de búsqueda, escriba **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-135">In the search box, type **Bynder**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="d0b28-137">En el panel de resultados, seleccione **Bynder** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0b28-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Selección de la aplicación en la galería](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="d0b28-139">Configuración y prueba del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="d0b28-140">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Microsoft Azure AD con Bynder con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d0b28-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0b28-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Bynder para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0b28-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="d0b28-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="d0b28-143">Esta relación de vínculo se establece asignando el valor de **nombre de usuario** en Azure AD como el valor de **nombre de usuario** en Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="d0b28-144">Para configurar y probar el inicio de sesión único de Microsoft Azure AD con Bynder, es preciso completar los bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d0b28-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0b28-145">**[Configuración del inicio de sesión único de Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**: para que los usuarios puedan usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d0b28-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0b28-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Microsoft Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0b28-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="d0b28-147">**[Creación de un usuario de prueba de Bynder](#creating-a-bynder-test-user)** : para tener un homólogo de Britta Simon en Bynder que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0b28-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d0b28-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para que Britta Simon pueda usar el inicio de sesión único de Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0b28-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="d0b28-149">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d0b28-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="d0b28-150">Configuración del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="d0b28-151">En esta sección, habilitará el inicio de sesión único de Microsoft Azure AD en el portal clásico y configurará el inicio de sesión único en la aplicación Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="d0b28-152">**Para configurar el inicio de sesión único de Microsoft Azure AD con Bynder, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d0b28-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="d0b28-153">En el portal clásico, en la página de integración de aplicaciones de **Bynder**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 
2. <span data-ttu-id="d0b28-155">En la página **¿Cómo desea que los usuarios inicien sesión en Bynder?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="d0b28-157">En el cuadro de diálogo **Configurar las opciones de la aplicación**, si desea configurar la aplicación en el **modo iniciado por el proveedor de identidades**, realice los pasos siguientes y haga clic en **Siguiente**:</span><span class="sxs-lookup"><span data-stu-id="d0b28-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="d0b28-159">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.getbynder.com/sso/SAML/authenticate/`.</span><span class="sxs-lookup"><span data-stu-id="d0b28-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="d0b28-160">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-160">Click **Next**.</span></span>
4. <span data-ttu-id="d0b28-161">Si quiere configurar la aplicación en el **modo iniciado por el proveedor de servicios**, en la página de diálogo **Configurar las opciones de la aplicación**, haga clic en **"Mostrar la configuración avanzada (opcional)"**, escriba la **URL de inicio de sesión** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="d0b28-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.getbynder.com/login/`.</span><span class="sxs-lookup"><span data-stu-id="d0b28-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="d0b28-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="d0b28-165">El valor de la dirección URL de inicio de sesión de este tutorial es solo un marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="d0b28-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="d0b28-166">Para obtener el valor real para su entorno, póngase en contacto con Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="d0b28-167">En la página **Configurar inicio de sesión único en Bynder**, realice los pasos siguientes y haga clic en **Siguiente**:</span><span class="sxs-lookup"><span data-stu-id="d0b28-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="d0b28-169">Haga clic en **Descargar metadatos**y luego guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d0b28-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d0b28-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-170">Click **Next**.</span></span>
6. <span data-ttu-id="d0b28-171">Para configurar el inicio de sesión único para la aplicación, póngase en contacto con el equipo de soporte técnico de Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="d0b28-172">Adjunte el archivo de metadatos descargado y compártalo con el equipo de Bynder para que le configure el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d0b28-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="d0b28-173">En el portal clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][10]
8. <span data-ttu-id="d0b28-175">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0b28-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-177">Create an Azure AD test user</span></span>
<span data-ttu-id="d0b28-178">El objetivo de esta sección es crear un usuario de prueba en el Portal clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0b28-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="d0b28-180">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d0b28-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0b28-181">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="d0b28-183">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="d0b28-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d0b28-184">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="d0b28-186">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="d0b28-188">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0b28-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="d0b28-190">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="d0b28-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d0b28-191">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d0b28-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-192">Click **Next**.</span></span>
6. <span data-ttu-id="d0b28-193">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0b28-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="d0b28-195">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d0b28-196">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="d0b28-197">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d0b28-198">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d0b28-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-199">Click **Next**.</span></span>
7. <span data-ttu-id="d0b28-200">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="d0b28-202">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0b28-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="d0b28-204">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="d0b28-205">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="d0b28-206">Creación de un usuario de prueba de Bynder</span><span class="sxs-lookup"><span data-stu-id="d0b28-206">Create a Bynder test user</span></span>
<span data-ttu-id="d0b28-207">El objetivo de esta sección es crear un usuario llamado Britta Simon en Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="d0b28-208">Bynder admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d0b28-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d0b28-209">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d0b28-209">There is no action item for you in this section.</span></span> <span data-ttu-id="d0b28-210">Durante un intento de acceder a Bynder se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="d0b28-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d0b28-211">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el equipo de soporte técnico de Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d0b28-212">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0b28-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="d0b28-213">El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure, para lo cual se le concederá acceso a Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Asignar usuario][200]

<span data-ttu-id="d0b28-215">**Para asignar a Britta Simon a Bynder, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d0b28-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="d0b28-216">En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="d0b28-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Asignar usuario][201]
2. <span data-ttu-id="d0b28-218">En la lista de aplicaciones, seleccione **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-218">In the applications list, select **Bynder**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="d0b28-220">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-220">In the menu on the top, click **Users**.</span></span>
   
    ![Asignar usuario][203]
4. <span data-ttu-id="d0b28-222">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d0b28-223">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="d0b28-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d0b28-225">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d0b28-225">Test single sign-on</span></span>
<span data-ttu-id="d0b28-226">El objetivo de esta sección es probar la configuración del inicio de sesión único de Microsoft Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d0b28-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d0b28-227">Al hacer clic en el icono de Bynder en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Bynder.</span><span class="sxs-lookup"><span data-stu-id="d0b28-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0b28-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d0b28-228">Additional resources</span></span>
* [<span data-ttu-id="d0b28-229">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0b28-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0b28-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0b28-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
