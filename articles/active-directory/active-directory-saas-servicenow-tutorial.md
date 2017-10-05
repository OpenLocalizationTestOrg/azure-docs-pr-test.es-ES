---
title: "Tutorial: Integración de Azure Active Directory con ServiceNow | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ServiceNow y ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="95248-103">Tutorial: Integración de Azure Active Directory con ServiceNow</span><span class="sxs-lookup"><span data-stu-id="95248-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="95248-104">En este tutorial, aprenderá a integrar ServiceNow y ServiceNow Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95248-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95248-105">La integración de ServiceNow y ServiceNow Express con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="95248-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="95248-106">En Azure AD se puede controlar quién tiene acceso a ServiceNow y ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="95248-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="95248-107">Puede permitir que los usuarios inicien sesión automáticamente en ServiceNow y ServiceNow Express (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95248-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="95248-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="95248-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="95248-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95248-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95248-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="95248-110">Prerequisites</span></span>
<span data-ttu-id="95248-111">Para configurar la integración de Azure AD con ServiceNow y ServiceNow Express se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="95248-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="95248-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95248-112">An Azure AD subscription</span></span>
* <span data-ttu-id="95248-113">Para ServiceNow, una instancia o inquilino de ServiceNow, versión Calgary o superior</span><span class="sxs-lookup"><span data-stu-id="95248-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="95248-114">Para ServiceNow Express, una instancia de ServiceNow Express, versión Helsinki o superior</span><span class="sxs-lookup"><span data-stu-id="95248-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="95248-115">El inquilino de ServiceNow debe tener habilitado el [complemento de inicio de sesión único en varios proveedores](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0).</span><span class="sxs-lookup"><span data-stu-id="95248-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="95248-116">Esto puede hacerse [enviando una solicitud de servicio](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="95248-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="95248-117">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="95248-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="95248-118">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="95248-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="95248-119">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="95248-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="95248-120">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95248-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95248-121">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="95248-121">Scenario description</span></span>
<span data-ttu-id="95248-122">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="95248-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95248-123">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="95248-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95248-124">Adición de ServiceNow desde la galería</span><span class="sxs-lookup"><span data-stu-id="95248-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="95248-125">Configuración y comprobación del inicio de sesión único de Azure AD en ServiceNow o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="95248-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="95248-126">Adición de ServiceNow desde la galería</span><span class="sxs-lookup"><span data-stu-id="95248-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="95248-127">Para configurar la integración de ServiceNow o ServiceNow Express en Azure AD, es preciso agregar ServiceNow desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="95248-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="95248-128">**Para agregar ServiceNow desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="95248-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95248-129">En el **Portal de Azure clásico**, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95248-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="95248-131">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="95248-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="95248-132">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="95248-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="95248-134">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="95248-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="95248-136">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="95248-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="95248-138">En el cuadro de búsqueda, escriba **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="95248-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="95248-140">En el panel de resultados, seleccione **ServiceNow** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95248-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95248-142">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95248-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95248-143">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ServiceNow o ServiceNow con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="95248-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95248-144">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ServiceNow para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95248-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="95248-145">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="95248-146">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="95248-147">Para configurar y probar el inicio de sesión único de Azure AD con ServiceNow, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="95248-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95248-148">**[Configuración del inicio de sesión único de Azure AD para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="95248-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95248-149">**[Configuración del inicio de sesión único de Azure AD para ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="95248-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="95248-150">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95248-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="95248-151">**[Creación de usuarios de prueba de ServiceNow](#creating-a-servicenow-test-user)**: para tener un homólogo de Britta Simon en ServiceNow que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95248-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="95248-152">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95248-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="95248-153">**[Prueba del inicio de sesión único](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="95248-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="95248-154">Si desea configurar ServiceNow, omita el paso 2.</span><span class="sxs-lookup"><span data-stu-id="95248-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="95248-155">De igual modo, si desea configurar ServiceNow Express, omita el paso 1.</span><span class="sxs-lookup"><span data-stu-id="95248-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="95248-156">Configuración del inicio de sesión único de Azure AD para ServiceNow</span><span class="sxs-lookup"><span data-stu-id="95248-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="95248-157">En el Portal de Azure AD clásico, en la página de integración de aplicaciones de **ServiceNow**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="95248-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="95248-158">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="95248-159">En la página **¿Cómo desea que los usuarios inicien sesión en ServiceNow?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="95248-160">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="95248-161">En la página **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="95248-162">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="95248-163">a.</span><span class="sxs-lookup"><span data-stu-id="95248-163">a.</span></span> <span data-ttu-id="95248-164">En el cuadro de texto **URL de inicio de sesión de ServiceNow**, escriba la dirección URL usada por los usuarios para iniciar sesión en la aplicación ServiceNow con el siguiente patrón: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="95248-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="95248-165">b.</span><span class="sxs-lookup"><span data-stu-id="95248-165">b.</span></span> <span data-ttu-id="95248-166">En el cuadro de texto **Identifier**, escriba la dirección URL usada por los usuarios para iniciar sesión en la aplicación ServiceNow con el siguiente patrón: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="95248-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="95248-167">c.</span><span class="sxs-lookup"><span data-stu-id="95248-167">c.</span></span> <span data-ttu-id="95248-168">Haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="95248-168">Click **Next**</span></span>

4. <span data-ttu-id="95248-169">Para que Azure AD configure automáticamente ServiceNow para la autenticación basada en SAML, escriba el nombre de la instancia de ServiceNow, el nombre de usuario de administrador y la contraseña de administrador en el formulario **Configurar el inicio de sesión único automáticamente** y haga clic en *Configurar*.</span><span class="sxs-lookup"><span data-stu-id="95248-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="95248-170">Tenga en cuenta que el nombre de usuario de administrador proporcionado debe tener asignado el rol **security_admin** en ServiceNow para que esto funcione.</span><span class="sxs-lookup"><span data-stu-id="95248-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="95248-171">De lo contrario, para configurar manualmente ServiceNow para usar Azure AD como proveedor de identidades SAML, haga clic en **Configurar manualmente esta aplicación para el inicio de sesión único** y en **Siguiente**, y complete los pasos indicados a continuación.</span><span class="sxs-lookup"><span data-stu-id="95248-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="95248-172">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="95248-173">En la página **Configurar inicio de sesión único en ServiceNow**, haga clic en **Descargar certificado**, guarde el archivo de certificado localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="95248-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="95248-174">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="95248-175">Inicie sesión en su aplicación ServiceNow como administrador.</span><span class="sxs-lookup"><span data-stu-id="95248-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="95248-176">Active el complemento *Integration - Multiple Provider Single Sign-On Installer*, para lo que debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95248-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="95248-177">a.</span><span class="sxs-lookup"><span data-stu-id="95248-177">a.</span></span> <span data-ttu-id="95248-178">En el panel de navegación del lado izquierdo, Vaya a la sección **System Definition** (Definición del sistema) y haga clic en **Plugins** (Complementos).</span><span class="sxs-lookup"><span data-stu-id="95248-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="95248-179">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")(Activar complemento)</span><span class="sxs-lookup"><span data-stu-id="95248-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="95248-180">b.</span><span class="sxs-lookup"><span data-stu-id="95248-180">b.</span></span> <span data-ttu-id="95248-181">Busque *Integration - Multiple Provider Single Sign-On Installer*.</span><span class="sxs-lookup"><span data-stu-id="95248-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="95248-182">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")(Activar complemento)</span><span class="sxs-lookup"><span data-stu-id="95248-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="95248-183">c.</span><span class="sxs-lookup"><span data-stu-id="95248-183">c.</span></span> <span data-ttu-id="95248-184">Seleccione el complemento.</span><span class="sxs-lookup"><span data-stu-id="95248-184">Select the plugin.</span></span> <span data-ttu-id="95248-185">Haga clic con el botón derecho y seleccione **Activate/Upgrade** (Activar o actualizar).</span><span class="sxs-lookup"><span data-stu-id="95248-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="95248-186">d.</span><span class="sxs-lookup"><span data-stu-id="95248-186">d.</span></span> <span data-ttu-id="95248-187">Haga clic en el botón **Activate**.</span><span class="sxs-lookup"><span data-stu-id="95248-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="95248-188">En el panel de navegación de la izquierda, haga clic en **Properties**(Propiedades).</span><span class="sxs-lookup"><span data-stu-id="95248-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="95248-189">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="95248-190">En el cuadro de diálogo **Multiple Provider SSO Properties** (Propiedades de SSO de varias proveedores), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="95248-191">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="95248-192">a.</span><span class="sxs-lookup"><span data-stu-id="95248-192">a.</span></span> <span data-ttu-id="95248-193">En **Enable multiple provider SSO** (Habilitar SSO de varios proveedores), seleccione **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="95248-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="95248-194">b.</span><span class="sxs-lookup"><span data-stu-id="95248-194">b.</span></span> <span data-ttu-id="95248-195">En **Enable debug logging got the multiple provider SSO integration** (Habilitar registro de depuración para integración de SSO de varios proveedores), seleccione **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="95248-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="95248-196">c.</span><span class="sxs-lookup"><span data-stu-id="95248-196">c.</span></span> <span data-ttu-id="95248-197">En el cuadro de texto **The field on the user table that...** (El campo en la tabla de usuario que...), escriba **user_name** (nombre_usuario).</span><span class="sxs-lookup"><span data-stu-id="95248-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="95248-198">d.</span><span class="sxs-lookup"><span data-stu-id="95248-198">d.</span></span> <span data-ttu-id="95248-199">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="95248-199">Click **Save**.</span></span>

10. <span data-ttu-id="95248-200">En el panel de navegación de la izquierda, haga clic en **Certificados x509**.</span><span class="sxs-lookup"><span data-stu-id="95248-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="95248-201">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="95248-202">En el cuadro de diálogo **Certificados X.509**, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="95248-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="95248-203">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="95248-204">En el cuadro de diálogo **Certificados X.509** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="95248-205">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="95248-206">a.</span><span class="sxs-lookup"><span data-stu-id="95248-206">a.</span></span> <span data-ttu-id="95248-207">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="95248-207">Click **New**.</span></span>
    
     <span data-ttu-id="95248-208">b.</span><span class="sxs-lookup"><span data-stu-id="95248-208">b.</span></span> <span data-ttu-id="95248-209">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración (por ejemplo, **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="95248-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="95248-210">c.</span><span class="sxs-lookup"><span data-stu-id="95248-210">c.</span></span> <span data-ttu-id="95248-211">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="95248-211">Select **Active**.</span></span>
    
     <span data-ttu-id="95248-212">d.</span><span class="sxs-lookup"><span data-stu-id="95248-212">d.</span></span> <span data-ttu-id="95248-213">En **Format** (Formato), seleccione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="95248-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="95248-214">e.</span><span class="sxs-lookup"><span data-stu-id="95248-214">e.</span></span> <span data-ttu-id="95248-215">En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).</span><span class="sxs-lookup"><span data-stu-id="95248-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="95248-216">f.</span><span class="sxs-lookup"><span data-stu-id="95248-216">f.</span></span> <span data-ttu-id="95248-217">Abra el certificado con codificación Base64 en el Bloc de notas, copie su contenido en el Portapapeles y péguelo en el cuadro de texto **PEM Certificate** (Certificado PEM).</span><span class="sxs-lookup"><span data-stu-id="95248-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="95248-218">g.</span><span class="sxs-lookup"><span data-stu-id="95248-218">g.</span></span> <span data-ttu-id="95248-219">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="95248-219">Click **Update**.</span></span>

13. <span data-ttu-id="95248-220">En el panel de navegación de la izquierda, haga clic en **Identity Providers**(Proveedores de identidades).</span><span class="sxs-lookup"><span data-stu-id="95248-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="95248-221">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="95248-222">En el cuadro de diálogo **Proveedores de identidades**, haga clic en **Nuevo**:</span><span class="sxs-lookup"><span data-stu-id="95248-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="95248-223">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="95248-224">En el cuadro de diálogo **Proveedores de identidades**, haga clic en **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="95248-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="95248-225">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="95248-226">En el cuadro de diálogo SAML2 Update1 Properties (Propiedades de SAML2 Update1), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="95248-227">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="95248-228">a.</span><span class="sxs-lookup"><span data-stu-id="95248-228">a.</span></span> <span data-ttu-id="95248-229">En el cuadro de texto **Nombre**, escriba el nombre de la configuración (por ejemplo, **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="95248-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="95248-230">b.</span><span class="sxs-lookup"><span data-stu-id="95248-230">b.</span></span> <span data-ttu-id="95248-231">En el cuadro de texto **Campo de usuario**, escriba **correo electrónico** o **user_name**, según qué campo se use para identificar de forma única a los usuarios en la implementación de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="95248-232">Puede configurar Azure AD para que emita el identificador de usuario de Azure AD (nombre principal de usuario) o la dirección de correo electrónico como identificador único en el token SAML. Para ello, vaya a la sección **ServiceNow > Atributos > Inicio de sesión único** en el Portal de Azure clásico y asigne el campo que desee al atributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="95248-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="95248-233">El valor almacenado para el atributo seleccionado en Azure AD (por ejemplo, nombre principal de usuario) debe coincidir con el valor almacenado en ServiceNow para el campo especificado (por ejemplo, user_name).</span><span class="sxs-lookup"><span data-stu-id="95248-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="95248-234">c.</span><span class="sxs-lookup"><span data-stu-id="95248-234">c.</span></span> <span data-ttu-id="95248-235">En el Portal de Azure AD clásico, copie el valor de **Id. de proveedor de identidad**y péguelo en el cuadro de texto **Identity Provider URL** (URL del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="95248-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="95248-236">d.</span><span class="sxs-lookup"><span data-stu-id="95248-236">d.</span></span> <span data-ttu-id="95248-237">En el Portal de Azure AD clásico, copie el valor de **Dirección URL de solicitud de autenticación** y péguelo en el cuadro de texto **Solicitud de autenticación de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="95248-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="95248-238">e.</span><span class="sxs-lookup"><span data-stu-id="95248-238">e.</span></span> <span data-ttu-id="95248-239">En el Portal de Azure AD clásico, copie el valor de **Dirección URL del servicio de cierre de sesión único** y péguelo en el cuadro de texto **Solicitud de cierre de sesión única del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="95248-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="95248-240">f.</span><span class="sxs-lookup"><span data-stu-id="95248-240">f.</span></span> <span data-ttu-id="95248-241">En el cuadro de texto **ServiceNow Homepage** (Página de inicio de ServiceNow), escriba la dirección URL de la página de inicio de instancia de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95248-242">La página de inicio de la instancia de ServiceNow es una concatenación de su **URL de inquilino de ServiceNow** y **/navpage.do** (por ejemplo: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="95248-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="95248-243">g.</span><span class="sxs-lookup"><span data-stu-id="95248-243">g.</span></span> <span data-ttu-id="95248-244">En el cuadro de texto **Entity ID / Issuer** (Id. de entidad / emisor), escriba la dirección URL de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="95248-245">h.</span><span class="sxs-lookup"><span data-stu-id="95248-245">h.</span></span> <span data-ttu-id="95248-246">En el cuadro de texto **Audience URL** (Dirección URL de audiencia), escriba la dirección URL de su inquilino ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="95248-247">i.</span><span class="sxs-lookup"><span data-stu-id="95248-247">i.</span></span> <span data-ttu-id="95248-248">En el cuadro de texto **Protocol Binding for the IDP's SingleLogoutRequest** (Vinculación de protocolo para la solicitud de cierre de sesión único del proveedor de identidades), escriba **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="95248-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="95248-249">j.</span><span class="sxs-lookup"><span data-stu-id="95248-249">j.</span></span> <span data-ttu-id="95248-250">En el cuadro de texto NameID Policy (Directiva de Id. de nombres), escriba **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="95248-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="95248-251">k.</span><span class="sxs-lookup"><span data-stu-id="95248-251">k.</span></span> <span data-ttu-id="95248-252">Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).</span><span class="sxs-lookup"><span data-stu-id="95248-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="95248-253">l.</span><span class="sxs-lookup"><span data-stu-id="95248-253">l.</span></span> <span data-ttu-id="95248-254">En **AuthnContextClassRef Method** (Método AuthnContextClassRef), escriba `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="95248-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="95248-255">Esto solo es preciso para las organizaciones que solo trabajan en la nube.</span><span class="sxs-lookup"><span data-stu-id="95248-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="95248-256">Si se usa MFA o ADFS local para la autenticación, este valor no se debe configurar.</span><span class="sxs-lookup"><span data-stu-id="95248-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="95248-257">m.</span><span class="sxs-lookup"><span data-stu-id="95248-257">m.</span></span> <span data-ttu-id="95248-258">En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.</span><span class="sxs-lookup"><span data-stu-id="95248-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="95248-259">n.</span><span class="sxs-lookup"><span data-stu-id="95248-259">n.</span></span> <span data-ttu-id="95248-260">En **Single Sign On Script** (Script de inicio de sesión único), seleccione **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="95248-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="95248-261">o.</span><span class="sxs-lookup"><span data-stu-id="95248-261">o.</span></span> <span data-ttu-id="95248-262">Como **Certificado X.509**, seleccione el certificado que ha creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="95248-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="95248-263">p.</span><span class="sxs-lookup"><span data-stu-id="95248-263">p.</span></span> <span data-ttu-id="95248-264">Haga clic en **Submit**(Enviar).</span><span class="sxs-lookup"><span data-stu-id="95248-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="95248-265">En el Portal de Azure AD clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="95248-266">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="95248-267">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="95248-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="95248-268">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="95248-269">Configuración del inicio de sesión único de Azure AD para ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="95248-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="95248-270">En el Portal de Azure AD clásico, en la página de integración de aplicaciones de **ServiceNow**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="95248-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="95248-271">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="95248-272">En la página **¿Cómo desea que los usuarios inicien sesión en ServiceNow?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="95248-273">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="95248-274">En la página **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="95248-275">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="95248-276">a.</span><span class="sxs-lookup"><span data-stu-id="95248-276">a.</span></span> <span data-ttu-id="95248-277">En el cuadro de texto **URL de inicio de sesión de ServiceNow**, escriba la dirección URL usada por los usuarios para iniciar sesión en la aplicación ServiceNow con el siguiente patrón: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="95248-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="95248-278">b.</span><span class="sxs-lookup"><span data-stu-id="95248-278">b.</span></span> <span data-ttu-id="95248-279">En el cuadro de texto **URL del emisor**, escriba la dirección URL usada por los usuarios para iniciar sesión en la aplicación ServiceNow con el siguiente patrón: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="95248-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="95248-280">c.</span><span class="sxs-lookup"><span data-stu-id="95248-280">c.</span></span> <span data-ttu-id="95248-281">Haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="95248-281">Click **Next**</span></span>

4. <span data-ttu-id="95248-282">Haga clic en **Configurar manualmente esta aplicación para el inicio de sesión único** y, luego, en **Siguiente**, y complete los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="95248-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="95248-283">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="95248-284">En la página **Configurar inicio de sesión único en ServiceNow**, haga clic en **Descargar certificado**, guarde el archivo de certificado localmente en el equipo y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="95248-285">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="95248-286">Inicie sesión en la aplicación ServiceNow Express como administrador.</span><span class="sxs-lookup"><span data-stu-id="95248-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="95248-287">En el panel de navegación del lado izquierdo, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="95248-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="95248-288">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="95248-289">En el cuadro de diálogo **Inicio de sesión único**, haga clic en el icono de configuración de la parte superior derecha y establezca las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="95248-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="95248-290">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="95248-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="95248-291">a.</span><span class="sxs-lookup"><span data-stu-id="95248-291">a.</span></span> <span data-ttu-id="95248-292">Cambie **Enable multiple provider SSO** (Habilitar SSO de varios proveedores), hacia la derecha.</span><span class="sxs-lookup"><span data-stu-id="95248-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="95248-293">b.</span><span class="sxs-lookup"><span data-stu-id="95248-293">b.</span></span> <span data-ttu-id="95248-294">Cambie **Enable debug logging got the multiple provider SSO integration** (Habilitar registro de depuración para integración de SSO de varios proveedores) hacia la derecha.</span><span class="sxs-lookup"><span data-stu-id="95248-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="95248-295">c.</span><span class="sxs-lookup"><span data-stu-id="95248-295">c.</span></span> <span data-ttu-id="95248-296">En el cuadro de texto **The field on the user table that...** (El campo en la tabla de usuario que...), escriba **user_name** (nombre_usuario).</span><span class="sxs-lookup"><span data-stu-id="95248-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="95248-297">En el cuadro de diálogo **Single Sign-On** (Inicio de sesión único), haga clic en **Add New Certificate** (Agregar nuevo certificado).</span><span class="sxs-lookup"><span data-stu-id="95248-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="95248-298">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="95248-299">En el cuadro de diálogo **Certificados X.509** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="95248-300">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="95248-301">a.</span><span class="sxs-lookup"><span data-stu-id="95248-301">a.</span></span> <span data-ttu-id="95248-302">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración (por ejemplo, **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="95248-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="95248-303">b.</span><span class="sxs-lookup"><span data-stu-id="95248-303">b.</span></span> <span data-ttu-id="95248-304">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="95248-304">Select **Active**.</span></span>
    
    <span data-ttu-id="95248-305">c.</span><span class="sxs-lookup"><span data-stu-id="95248-305">c.</span></span> <span data-ttu-id="95248-306">En **Format** (Formato), seleccione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="95248-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="95248-307">d.</span><span class="sxs-lookup"><span data-stu-id="95248-307">d.</span></span> <span data-ttu-id="95248-308">En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).</span><span class="sxs-lookup"><span data-stu-id="95248-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="95248-309">e.</span><span class="sxs-lookup"><span data-stu-id="95248-309">e.</span></span> <span data-ttu-id="95248-310">Cree un archivo con codificación Base64 a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="95248-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="95248-311">Para más información, vea [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="95248-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="95248-312">f.</span><span class="sxs-lookup"><span data-stu-id="95248-312">f.</span></span> <span data-ttu-id="95248-313">Abra el certificado con codificación Base64 en el Bloc de notas, copie su contenido en el Portapapeles y péguelo en el cuadro de texto **PEM Certificate** (Certificado PEM).</span><span class="sxs-lookup"><span data-stu-id="95248-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="95248-314">g.</span><span class="sxs-lookup"><span data-stu-id="95248-314">g.</span></span> <span data-ttu-id="95248-315">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="95248-315">Click **Update**.</span></span>
11. <span data-ttu-id="95248-316">En el cuadro de diálogo **Single Sign-On** (Inicio de sesión único), haga clic en **Add New IdP** (Agregar nuevo IdP).</span><span class="sxs-lookup"><span data-stu-id="95248-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="95248-317">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="95248-318">En el cuadro de diálogo **Add New Identity Provider** (Agregar nuevo proveedor de identidades), en **Configure Identity Provider** (Configurar proveedor de identidades), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95248-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="95248-319">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="95248-320">a.</span><span class="sxs-lookup"><span data-stu-id="95248-320">a.</span></span> <span data-ttu-id="95248-321">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración (por ejemplo, **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="95248-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="95248-322">b.</span><span class="sxs-lookup"><span data-stu-id="95248-322">b.</span></span> <span data-ttu-id="95248-323">En el Portal de Azure AD clásico, copie el valor de **Id. de proveedor de identidad**y péguelo en el cuadro de texto **Identity Provider URL** (URL del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="95248-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="95248-324">c.</span><span class="sxs-lookup"><span data-stu-id="95248-324">c.</span></span> <span data-ttu-id="95248-325">En el Portal de Azure AD clásico, copie el valor de **Dirección URL de solicitud de autenticación** y péguelo en el cuadro de texto **Solicitud de autenticación de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="95248-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="95248-326">d.</span><span class="sxs-lookup"><span data-stu-id="95248-326">d.</span></span> <span data-ttu-id="95248-327">En el Portal de Azure AD clásico, copie el valor de **Dirección URL del servicio de cierre de sesión único** y péguelo en el cuadro de texto **Solicitud de cierre de sesión única del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="95248-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="95248-328">e.</span><span class="sxs-lookup"><span data-stu-id="95248-328">e.</span></span> <span data-ttu-id="95248-329">Como **Certificado de proveedor de identidades**, seleccione el certificado que ha creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="95248-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="95248-330">Haga clic en **Advanced Settings** (Configuración avanzada) y en **Additional Identity Provider Properties** (Propiedades adicionales del proveedor de identidades), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95248-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="95248-331">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="95248-332">a.</span><span class="sxs-lookup"><span data-stu-id="95248-332">a.</span></span> <span data-ttu-id="95248-333">En el cuadro de texto **Protocol Binding for the IDP's SingleLogoutRequest** (Vinculación de protocolo para la solicitud de cierre de sesión único del proveedor de identidades), escriba **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="95248-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="95248-334">b.</span><span class="sxs-lookup"><span data-stu-id="95248-334">b.</span></span> <span data-ttu-id="95248-335">En el cuadro de texto **NameID Policy** (Directiva NameID), escriba **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="95248-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="95248-336">c.</span><span class="sxs-lookup"><span data-stu-id="95248-336">c.</span></span> <span data-ttu-id="95248-337">En **AuthnContextClassRef Method**, escriba **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="95248-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="95248-338">d.</span><span class="sxs-lookup"><span data-stu-id="95248-338">d.</span></span> <span data-ttu-id="95248-339">Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).</span><span class="sxs-lookup"><span data-stu-id="95248-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="95248-340">En **Additional Identity Provider Properties** (Propiedades adicionales del proveedor de identidades), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95248-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="95248-341">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="95248-342">a.</span><span class="sxs-lookup"><span data-stu-id="95248-342">a.</span></span> <span data-ttu-id="95248-343">En el cuadro de texto **ServiceNow Homepage** (Página de inicio de ServiceNow), escriba la dirección URL de la página de inicio de instancia de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="95248-344">La página de inicio de la instancia de ServiceNow es una concatenación de su **URL de inquilino de ServiceNow** y **/navpage.do** (por ejemplo: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="95248-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="95248-345">b.</span><span class="sxs-lookup"><span data-stu-id="95248-345">b.</span></span> <span data-ttu-id="95248-346">En el cuadro de texto **Entity ID / Issuer** (Id. de entidad / emisor), escriba la dirección URL de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="95248-347">c.</span><span class="sxs-lookup"><span data-stu-id="95248-347">c.</span></span> <span data-ttu-id="95248-348">En el cuadro de texto **Audience URI** (Identificador URI de audiencia), escriba la dirección URL de su inquilino ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="95248-349">d.</span><span class="sxs-lookup"><span data-stu-id="95248-349">d.</span></span> <span data-ttu-id="95248-350">En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.</span><span class="sxs-lookup"><span data-stu-id="95248-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="95248-351">e.</span><span class="sxs-lookup"><span data-stu-id="95248-351">e.</span></span> <span data-ttu-id="95248-352">En el cuadro de texto **Campo de usuario**, escriba **correo electrónico** o **user_name**, según qué campo se use para identificar de forma única a los usuarios en la implementación de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="95248-353">Puede configurar Azure AD para que emita el identificador de usuario de Azure AD (nombre principal de usuario) o la dirección de correo electrónico como identificador único en el token SAML. Para ello, vaya a la sección **ServiceNow > Atributos > Inicio de sesión único** en el Portal de Azure clásico y asigne el campo que desee al atributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="95248-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="95248-354">El valor almacenado para el atributo seleccionado en Azure AD (por ejemplo, nombre principal de usuario) debe coincidir con el valor almacenado en ServiceNow para el campo especificado (por ejemplo, user_name).</span><span class="sxs-lookup"><span data-stu-id="95248-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="95248-355">f.</span><span class="sxs-lookup"><span data-stu-id="95248-355">f.</span></span> <span data-ttu-id="95248-356">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="95248-356">Click **Save**.</span></span> 

3. <span data-ttu-id="95248-357">En el Portal de Azure AD clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="95248-358">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="95248-359">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="95248-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="95248-360">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="95248-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="95248-361">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="95248-361">Configuring user provisioning</span></span>
<span data-ttu-id="95248-362">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de cuentas de usuario de Active Directory para ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="95248-363">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="95248-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="95248-364">En el Portal de administración de Azure clásico, en la página de integración de la aplicación de **ServiceNow**, haga clic en **Configurar aprovisionamiento de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="95248-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="95248-365">![Aprovisionamiento de usuarios](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="95248-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="95248-366">En la página **Especifique sus credenciales de ServiceNow para habilitar el aprovisionamiento automático de usuarios**, proporcione los valores de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="95248-367">a.</span><span class="sxs-lookup"><span data-stu-id="95248-367">a.</span></span> <span data-ttu-id="95248-368">En el cuadro de texto **Nombre de la instancia de ServiceNow** , escriba el nombre de la instancia de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="95248-369">b.</span><span class="sxs-lookup"><span data-stu-id="95248-369">b.</span></span> <span data-ttu-id="95248-370">En el cuadro de texto **Nombre del usuario administrador de ServiceNow** , escriba el nombre de la cuenta de administrador de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="95248-371">c.</span><span class="sxs-lookup"><span data-stu-id="95248-371">c.</span></span> <span data-ttu-id="95248-372">En el cuadro de texto **Contraseña de administración de ServiceNow** , escriba la contraseña para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="95248-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="95248-373">d.</span><span class="sxs-lookup"><span data-stu-id="95248-373">d.</span></span> <span data-ttu-id="95248-374">Haga clic en **validar** para comprobar la configuración.</span><span class="sxs-lookup"><span data-stu-id="95248-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="95248-375">e.</span><span class="sxs-lookup"><span data-stu-id="95248-375">e.</span></span> <span data-ttu-id="95248-376">Haga clic en el botón **Siguiente** para abrir la página **Pasos siguientes**.</span><span class="sxs-lookup"><span data-stu-id="95248-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="95248-377">f.</span><span class="sxs-lookup"><span data-stu-id="95248-377">f.</span></span> <span data-ttu-id="95248-378">Si quiere aprovisionar todos los usuarios para esta aplicación, seleccione**Aprovisionar automáticamente todas las cuentas del directorio en esta aplicación**.</span><span class="sxs-lookup"><span data-stu-id="95248-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="95248-379">![Pasos siguientes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Pasos siguientes")</span><span class="sxs-lookup"><span data-stu-id="95248-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="95248-380">g.</span><span class="sxs-lookup"><span data-stu-id="95248-380">g.</span></span> <span data-ttu-id="95248-381">En la página **Pasos siguientes**, haga clic en **Completar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="95248-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95248-382">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95248-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="95248-383">En esta sección, creará un usuario de prueba llamado Britta Simon en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="95248-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="95248-385">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="95248-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95248-386">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95248-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="95248-388">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="95248-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="95248-389">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="95248-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95248-391">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="95248-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="95248-393">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="95248-395">a.</span><span class="sxs-lookup"><span data-stu-id="95248-395">a.</span></span> <span data-ttu-id="95248-396">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="95248-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="95248-397">b.</span><span class="sxs-lookup"><span data-stu-id="95248-397">b.</span></span> <span data-ttu-id="95248-398">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95248-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="95248-399">c.</span><span class="sxs-lookup"><span data-stu-id="95248-399">c.</span></span> <span data-ttu-id="95248-400">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-400">Click **Next**.</span></span>

6. <span data-ttu-id="95248-401">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="95248-403">a.</span><span class="sxs-lookup"><span data-stu-id="95248-403">a.</span></span> <span data-ttu-id="95248-404">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="95248-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="95248-405">b.</span><span class="sxs-lookup"><span data-stu-id="95248-405">b.</span></span> <span data-ttu-id="95248-406">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="95248-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="95248-407">c.</span><span class="sxs-lookup"><span data-stu-id="95248-407">c.</span></span> <span data-ttu-id="95248-408">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="95248-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="95248-409">d.</span><span class="sxs-lookup"><span data-stu-id="95248-409">d.</span></span> <span data-ttu-id="95248-410">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="95248-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="95248-411">e.</span><span class="sxs-lookup"><span data-stu-id="95248-411">e.</span></span> <span data-ttu-id="95248-412">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="95248-412">Click **Next**.</span></span>

7. <span data-ttu-id="95248-413">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="95248-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="95248-415">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95248-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="95248-417">a.</span><span class="sxs-lookup"><span data-stu-id="95248-417">a.</span></span> <span data-ttu-id="95248-418">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="95248-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="95248-419">b.</span><span class="sxs-lookup"><span data-stu-id="95248-419">b.</span></span> <span data-ttu-id="95248-420">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="95248-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="95248-421">Creación de un usuario de prueba de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="95248-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="95248-422">En esta sección, creará un usuario llamado Britta Simon en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="95248-423">En esta sección, creará un usuario llamado Britta Simon en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="95248-424">Si no sabe cómo agregar un usuario en una cuenta de ServiceNow o ServiceNow Express, póngase en contacto con el equipo de soporte técnico de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="95248-425">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95248-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="95248-426">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="95248-428">**Para asignar Britta Simon a ServiceNow, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="95248-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="95248-429">En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="95248-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Asignar usuario][201] 

2. <span data-ttu-id="95248-431">En la lista de aplicaciones, seleccione **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="95248-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="95248-433">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="95248-433">In the menu on the top, click **Users**.</span></span>
   
    ![Asignar usuario][203] 

4. <span data-ttu-id="95248-435">En la lista Todos los usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="95248-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="95248-436">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="95248-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="95248-438">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="95248-438">Testing single sign-on</span></span>
<span data-ttu-id="95248-439">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="95248-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="95248-440">Al hacer clic en el icono de ServiceNow en el panel de acceso, debería iniciar sesión automáticamente en su aplicación ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="95248-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95248-441">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="95248-441">Additional resources</span></span>
* [<span data-ttu-id="95248-442">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95248-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95248-443">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95248-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
