---
title: "Tutorial: Integración de Azure Active Directory con Wizergos Productivity Software | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Wizergos Productivity Software."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="a4163-103">Tutorial: integración de Azure Active Directory con Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="a4163-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="a4163-104">El objetivo de este tutorial es mostrar cómo integrar Wizergos Productivity Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4163-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4163-105">La integración de Wizergos Productivity Software con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a4163-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="a4163-106">Puede controlar en Azure AD quién tiene acceso a Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="a4163-107">Puede permitir que los usuarios inicien sesión automáticamente en Wizergos Productivity Software (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a4163-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="a4163-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="a4163-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4163-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4163-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a4163-110">Prerequisites</span></span>
<span data-ttu-id="a4163-111">Para configurar la integración de Azure AD con Wizergos Productivity Software, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a4163-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="a4163-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a4163-113">Un suscripción habilitada para el inicio de sesión único en Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="a4163-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a4163-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a4163-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="a4163-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a4163-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a4163-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a4163-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a4163-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4163-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4163-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a4163-118">Scenario description</span></span>
<span data-ttu-id="a4163-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a4163-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="a4163-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a4163-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4163-121">Incorporación de Wizergos Productivity Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="a4163-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="a4163-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="a4163-123">Incorporación de Wizergos Productivity Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="a4163-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="a4163-124">Para configurar la integración de Wizergos Productivity Software en Azure AD, deberá agregar Wizergos Productivity Software desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a4163-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a4163-125">**Para agregar Wizergos Productivity Software desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a4163-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a4163-126">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4163-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a4163-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="a4163-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a4163-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="a4163-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="a4163-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="a4163-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="a4163-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="a4163-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="a4163-135">En el cuadro de búsqueda, escriba **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="a4163-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="a4163-137">En el panel de resultados, seleccione **Wizergos Productivity Software** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4163-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Selección de la aplicación en la galería](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="a4163-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="a4163-140">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con Wizergos Productivity Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a4163-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4163-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Wizergos Productivity Software para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="a4163-142">En otras palabras, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="a4163-143">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="a4163-144">Para configurar y probar el inicio de sesión único de Azure AD con Wizergos Productivity Software, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a4163-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4163-145">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a4163-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4163-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4163-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4163-147">**[Creación de un usuario de prueba de Wizergos Productivity Software](#creating-a-wizergos-productivity-software-test-user)** : para tener un homólogo de Britta Simon en Wizergos Productivity Software que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a4163-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4163-149">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a4163-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="a4163-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="a4163-151">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal clásico y configurará el inicio de sesión único en la aplicación Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="a4163-152">**Para configurar el inicio de sesión único de Azure AD con Wizergos Productivity Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a4163-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="a4163-153">En el portal clásico, en la página de integración de aplicaciones de **Wizergos Productivity Software**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a4163-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 
2. <span data-ttu-id="a4163-155">En la página **¿Cómo desea que los usuarios inicien sesión en Wizergos Productivity Software?**, seleccione **Inicio de sesión único de Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4163-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="a4163-157">En la página de diálogo **Configurar las opciones de la aplicación**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4163-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="a4163-159">En la página **Configuración de inicio de sesión único en Wizergos Productivity Software**, haga clic en **Descargar certificado** y guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a4163-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="a4163-161">En otra ventana del explorador web, inicie sesión en su inquilino de Wizergos Productivity Software como administrador.</span><span class="sxs-lookup"><span data-stu-id="a4163-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="a4163-162">En el menú lateral, seleccione **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a4163-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="a4163-164">En el menú de la izquierda de la página Admin, seleccione **AUTHENTICACIÓN** y haga clic en **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="a4163-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="a4163-166">En la sección **AUTHENTICACIÓN** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4163-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="a4163-168">Para cargar el certificado descargado de Azure AD, haga clic en **UPLOAD** (Cargar).</span><span class="sxs-lookup"><span data-stu-id="a4163-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="a4163-169">En el cuadro de texto **URL del emisor**, coloque el valor de **URL del emisor** del Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="a4163-170">En el cuadro de texto **Dirección URL de inicio de sesión único**, coloque el valor de **Dirección URL del servicio de inicio de sesión único** en el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="a4163-171">En el cuadro de texto **Dirección URL de inicio de sesión único**, coloque el valor de **Dirección URL del servicio de cierre de sesión único** en el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4163-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="a4163-172">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a4163-172">Click **Save** button.</span></span>
9. <span data-ttu-id="a4163-173">En el Portal clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4163-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][10]
10. <span data-ttu-id="a4163-175">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="a4163-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a4163-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-177">Create an Azure AD test user</span></span>
<span data-ttu-id="a4163-178">El objetivo de esta sección es crear un usuario de prueba en el Portal clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4163-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="a4163-180">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a4163-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4163-181">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4163-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="a4163-183">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="a4163-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a4163-184">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a4163-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="a4163-186">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="a4163-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="a4163-188">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4163-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="a4163-190">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="a4163-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="a4163-191">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4163-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="a4163-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4163-192">Click **Next**.</span></span>
6. <span data-ttu-id="a4163-193">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4163-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="a4163-195">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a4163-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="a4163-196">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4163-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="a4163-197">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4163-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="a4163-198">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="a4163-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="a4163-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4163-199">Click **Next**.</span></span>
7. <span data-ttu-id="a4163-200">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a4163-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="a4163-202">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4163-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="a4163-204">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a4163-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="a4163-205">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="a4163-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="a4163-206">Creación de un usuario de prueba de Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="a4163-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="a4163-207">En esta sección, creará un usuario llamado Britta Simon en Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="a4163-208">Trabaje con el equipo de soporte técnico de Wizergos Productivity Software mediante [support@wizergos.com](emailTo:support@wizergos.com) para agregar los usuarios a la plataforma Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a4163-209">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4163-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="a4163-210">El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure, para lo cual se le concederá acceso a Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Asignar usuario][200]

<span data-ttu-id="a4163-212">**Para asignar a Britta Simon a Wizergos Productivity Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a4163-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="a4163-213">En el Portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="a4163-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Asignar usuario][201]
2. <span data-ttu-id="a4163-215">En la lista de aplicaciones, seleccione **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="a4163-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="a4163-217">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a4163-217">In the menu on the top, click **Users**.</span></span>
   
    ![Asignar usuario][203]
4. <span data-ttu-id="a4163-219">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4163-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a4163-220">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="a4163-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a4163-222">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a4163-222">Test single sign-on</span></span>
<span data-ttu-id="a4163-223">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a4163-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a4163-224">Al hacer clic en el icono de Wizergos Productivity Software del panel de acceso, debería iniciar sesión automáticamente en su aplicación Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="a4163-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4163-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a4163-225">Additional resources</span></span>
* [<span data-ttu-id="a4163-226">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4163-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4163-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4163-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
