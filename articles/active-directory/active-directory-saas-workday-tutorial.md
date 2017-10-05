---
title: "Tutorial: Integración de Azure Active Directory con Workday | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workday."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="81ac8-103">Tutorial: Integración de Azure Active Directory con Workday</span><span class="sxs-lookup"><span data-stu-id="81ac8-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="81ac8-104">En este tutorial, obtendrá información sobre cómo integrar Workday con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81ac8-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81ac8-105">La integración de Workday con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="81ac8-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81ac8-106">Puede controlar en Azure AD quién tiene acceso a Workday.</span><span class="sxs-lookup"><span data-stu-id="81ac8-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="81ac8-107">Puede permitir que los usuarios inicien sesión automáticamente en Workday (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ac8-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81ac8-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81ac8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81ac8-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81ac8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ac8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81ac8-110">Prerequisites</span></span>

<span data-ttu-id="81ac8-111">Para configurar la integración de Azure AD con Workday, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="81ac8-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="81ac8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81ac8-113">Una suscripción habilitada para el inicio de sesión único en Workday</span><span class="sxs-lookup"><span data-stu-id="81ac8-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81ac8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="81ac8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81ac8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="81ac8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81ac8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81ac8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81ac8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81ac8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81ac8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="81ac8-118">Scenario description</span></span>
<span data-ttu-id="81ac8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="81ac8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81ac8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="81ac8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81ac8-121">Incorporación de Workday desde la galería</span><span class="sxs-lookup"><span data-stu-id="81ac8-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="81ac8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="81ac8-123">Incorporación de Workday desde la galería</span><span class="sxs-lookup"><span data-stu-id="81ac8-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="81ac8-124">Para configurar la integración de Workday en Azure AD, hay que agregar Workday desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="81ac8-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81ac8-125">**Para agregar Workday desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81ac8-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81ac8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81ac8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81ac8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="81ac8-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ac8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="81ac8-133">En el cuadro de búsqueda, escriba **Workday**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-133">In the search box, type **Workday**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="81ac8-135">En el panel de resultados, seleccione **Workday** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81ac8-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81ac8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81ac8-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Workday con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81ac8-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81ac8-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workday para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ac8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="81ac8-140">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workday.</span><span class="sxs-lookup"><span data-stu-id="81ac8-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="81ac8-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Workday.</span><span class="sxs-lookup"><span data-stu-id="81ac8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="81ac8-142">Para configurar y probar el inicio de sesión único de Azure AD con Workday, hay que completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="81ac8-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81ac8-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="81ac8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81ac8-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81ac8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81ac8-145">**[Creación de un usuario de prueba de Workday](#creating-a-workday-test-user)**: para tener un homólogo de Britta Simon en Workday que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ac8-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81ac8-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ac8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81ac8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="81ac8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81ac8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81ac8-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Workday.</span><span class="sxs-lookup"><span data-stu-id="81ac8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="81ac8-150">**Para configurar el inicio de sesión único de Azure AD con Workday, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81ac8-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="81ac8-151">En Azure Portal, en la página de integración de la aplicación **Workday**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="81ac8-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="81ac8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="81ac8-155">En la sección **Dominio y direcciones URL de Workday**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81ac8-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="81ac8-157">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-157">a.</span></span> <span data-ttu-id="81ac8-158">En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="81ac8-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="81ac8-159">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-159">b.</span></span> <span data-ttu-id="81ac8-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://impl.workday.com/<tenant>/login-saml.htmld`.</span><span class="sxs-lookup"><span data-stu-id="81ac8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81ac8-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="81ac8-161">These values are not the real.</span></span> <span data-ttu-id="81ac8-162">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="81ac8-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="81ac8-163">La URL de respuesta debe tener un subdominio (por ejemplo, www, wd2, wd3, wd3-impl, wd5 y wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="81ac8-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="81ac8-164">Usar algo como "*http://www.myworkday.com*" funciona, pero "*http://myworkday.com*" no funciona.</span><span class="sxs-lookup"><span data-stu-id="81ac8-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="81ac8-165">Póngase en contacto con el [equipo de soporte técnico de Workday](https://www.workday.com/en-us/partners-services/services/support.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="81ac8-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="81ac8-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="81ac8-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="81ac8-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="81ac8-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81ac8-170">En la sección **Configuración de Workday**, haga clic en **Configurar Workday** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81ac8-171">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="81ac8-172">![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="81ac8-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="81ac8-173">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Workday como administrador.</span><span class="sxs-lookup"><span data-stu-id="81ac8-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="81ac8-174">Vaya a **Menú \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="81ac8-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="81ac8-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="81ac8-176">Vaya a **Administración de cuentas**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="81ac8-177">![Administración de cuentas](./media/active-directory-saas-workday-tutorial/IC782924.png "Administración de cuentas")</span><span class="sxs-lookup"><span data-stu-id="81ac8-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="81ac8-178">Vaya a **Editar configuración de inquilino: Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="81ac8-179">![Edición de seguridad del inquilino](./media/active-directory-saas-workday-tutorial/IC782925.png "Edición de seguridad del inquilino")</span><span class="sxs-lookup"><span data-stu-id="81ac8-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="81ac8-180">En la sección **URL de redireccionamiento** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="81ac8-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="81ac8-181">![Direcciones URL de redirección](./media/active-directory-saas-workday-tutorial/IC7829581.png "Direcciones URL de redirección")</span><span class="sxs-lookup"><span data-stu-id="81ac8-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="81ac8-182">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-182">a.</span></span> <span data-ttu-id="81ac8-183">Haga clic en **Add Row**(Agregar fila).</span><span class="sxs-lookup"><span data-stu-id="81ac8-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="81ac8-184">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-184">b.</span></span> <span data-ttu-id="81ac8-185">En los cuadros de texto **Dirección URL de redireccionamiento de inicio de sesión** y **URL de redireccionamiento móvil**, escriba la **dirección URL de inicio de sesión** que ha especificado en la sección **Dominio y direcciones URL de Workday** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81ac8-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="81ac8-186">c.</span><span class="sxs-lookup"><span data-stu-id="81ac8-186">c.</span></span> <span data-ttu-id="81ac8-187">En la ventana **Configurar inicio de sesión único** de Azure Portal, copie la **dirección URL de cierre de sesión único** y péguela en el cuadro de texto **Logout Redirect URL** (URL de redireccionamiento de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="81ac8-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="81ac8-188">d.</span><span class="sxs-lookup"><span data-stu-id="81ac8-188">d.</span></span>  <span data-ttu-id="81ac8-189">En el cuadro de texto **Entorno** , escriba el nombre del entorno.</span><span class="sxs-lookup"><span data-stu-id="81ac8-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="81ac8-190">El valor del atributo Entorno está vinculado con el valor de la URL del inquilino:</span><span class="sxs-lookup"><span data-stu-id="81ac8-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="81ac8-191">Si el nombre de dominio de la URL de inquilino de Workday empieza por impl (por ejemplo, *https://impl.workday.com/\<inquilino\>/login-saml2.htmld*), el atributo **Entorno** tiene que establecerse en Implementación.</span><span class="sxs-lookup"><span data-stu-id="81ac8-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="81ac8-192">Si el nombre de dominio empieza por otra cosa, deberá ponerse en contacto con el [equipo de soporte técnico de Workday](https://www.workday.com/en-us/partners-services/services/support.html) para obtener el valor de **Entorno** coincidente.</span><span class="sxs-lookup"><span data-stu-id="81ac8-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="81ac8-193">En la sección **Configuración de SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81ac8-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="81ac8-194">![Configuración de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="81ac8-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="81ac8-195">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-195">a.</span></span>  <span data-ttu-id="81ac8-196">Seleccione **Enable SAML Authentication**(Habilitar autenticación SAML).</span><span class="sxs-lookup"><span data-stu-id="81ac8-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="81ac8-197">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-197">b.</span></span>  <span data-ttu-id="81ac8-198">Haga clic en **Add Row**(Agregar fila).</span><span class="sxs-lookup"><span data-stu-id="81ac8-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="81ac8-199">En la sección Proveedores de identidades SAML, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81ac8-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="81ac8-200">![Proveedores de identidades SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Proveedores de identidades SAML")</span><span class="sxs-lookup"><span data-stu-id="81ac8-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="81ac8-201">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-201">a.</span></span> <span data-ttu-id="81ac8-202">En el cuadro de texto Nombre del proveedor de identidad, escriba un nombre de proveedor (por ejemplo, *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="81ac8-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="81ac8-203">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-203">b.</span></span> <span data-ttu-id="81ac8-204">En la ventana **Configurar inicio de sesión único** de Azure Portal, copie el valor de **SAML Entity ID** (Identificador de entidad de SAML) y, luego, péguelo en el cuadro de texto **Emisor**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="81ac8-205">c.</span><span class="sxs-lookup"><span data-stu-id="81ac8-205">c.</span></span> <span data-ttu-id="81ac8-206">Seleccione **Enable Workday Initiated Logout** (Habilitar el cierre de sesión iniciado de Workday).</span><span class="sxs-lookup"><span data-stu-id="81ac8-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="81ac8-207">d.</span><span class="sxs-lookup"><span data-stu-id="81ac8-207">d.</span></span> <span data-ttu-id="81ac8-208">En la ventana **Configurar inicio de sesión único** de Azure Portal, copie el valor de **Dirección URL de cierre de sesión** y péguela en el cuadro de texto **Logout Request URL** (URL de solicitud de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="81ac8-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="81ac8-209">e.</span><span class="sxs-lookup"><span data-stu-id="81ac8-209">e.</span></span> <span data-ttu-id="81ac8-210">Haga clic en **Identity Provider Public Key Certificate** (Certificado de clave pública de proveedor de identidades) y, después, en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="81ac8-211">![Crear](./media/active-directory-saas-workday-tutorial/IC782928.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="81ac8-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="81ac8-212">f.</span><span class="sxs-lookup"><span data-stu-id="81ac8-212">f.</span></span> <span data-ttu-id="81ac8-213">Haga clic en **Create x509 Public Key**(Crear clave pública x509).</span><span class="sxs-lookup"><span data-stu-id="81ac8-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="81ac8-214">![Crear](./media/active-directory-saas-workday-tutorial/IC782929.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="81ac8-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="81ac8-215">En la sección **View x509 Public Key** (Ver clave pública x509), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="81ac8-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="81ac8-216">![Visualización de clave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Visualización de clave pública x509")</span><span class="sxs-lookup"><span data-stu-id="81ac8-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="81ac8-217">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-217">a.</span></span> <span data-ttu-id="81ac8-218">En el cuadro de texto **Nombre**, escriba el nombre del certificado (por ejemplo, *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="81ac8-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="81ac8-219">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-219">b.</span></span> <span data-ttu-id="81ac8-220">En el cuadro de texto **Válido desde** , escriba el valor del atributo Válido desde del certificado.</span><span class="sxs-lookup"><span data-stu-id="81ac8-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="81ac8-221">c.</span><span class="sxs-lookup"><span data-stu-id="81ac8-221">c.</span></span>  <span data-ttu-id="81ac8-222">En el cuadro de texto **Válido hasta** , escriba el valor del atributo Válido hasta del certificado.</span><span class="sxs-lookup"><span data-stu-id="81ac8-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="81ac8-223">Puede obtener la fecha válido desde y la fecha válido hasta del certificado descargado haciendo doble clic en él.</span><span class="sxs-lookup"><span data-stu-id="81ac8-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="81ac8-224">Las fechas se muestran bajo la pestaña **Detalles** .</span><span class="sxs-lookup"><span data-stu-id="81ac8-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="81ac8-225">d.</span><span class="sxs-lookup"><span data-stu-id="81ac8-225">d.</span></span>  <span data-ttu-id="81ac8-226">Abra el certificado codificado en base 64 en el Bloc de notas y luego copie el contenido del mismo.</span><span class="sxs-lookup"><span data-stu-id="81ac8-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="81ac8-227">e.</span><span class="sxs-lookup"><span data-stu-id="81ac8-227">e.</span></span>  <span data-ttu-id="81ac8-228">En el cuadro de texto **Certificado** , pegue el contenido del portapapeles.</span><span class="sxs-lookup"><span data-stu-id="81ac8-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="81ac8-229">f.</span><span class="sxs-lookup"><span data-stu-id="81ac8-229">f.</span></span>  <span data-ttu-id="81ac8-230">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-230">Click **OK**.</span></span>

15. <span data-ttu-id="81ac8-231">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="81ac8-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="81ac8-232">![Configuración de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="81ac8-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="81ac8-233">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-233">a.</span></span>  <span data-ttu-id="81ac8-234">Habilite el **par de claves privadas x509**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="81ac8-235">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-235">b.</span></span>  <span data-ttu-id="81ac8-236">En el cuadro de texto **Id. de proveedor de servicios**, escriba **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="81ac8-237">c.</span><span class="sxs-lookup"><span data-stu-id="81ac8-237">c.</span></span>  <span data-ttu-id="81ac8-238">Seleccione **Habilitar autenticación SAML iniciada por el proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="81ac8-239">d.</span><span class="sxs-lookup"><span data-stu-id="81ac8-239">d.</span></span>  <span data-ttu-id="81ac8-240">En la ventana **Configurar inicio de sesión único** de Azure Portal, copie el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) y péguelo en el cuadro de texto **IdP SSO Service URL** (URL de servicio SSO de IdP).</span><span class="sxs-lookup"><span data-stu-id="81ac8-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="81ac8-241">e.</span><span class="sxs-lookup"><span data-stu-id="81ac8-241">e.</span></span> <span data-ttu-id="81ac8-242">Seleccione **No desinflar la solicitud de autenticación iniciada por el SP**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="81ac8-243">f.</span><span class="sxs-lookup"><span data-stu-id="81ac8-243">f.</span></span> <span data-ttu-id="81ac8-244">Como **Método de firma de solicitud de autenticación**, seleccione **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="81ac8-245">![Método de firma de solicitud de autenticación](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de firma de solicitud de autenticación")</span><span class="sxs-lookup"><span data-stu-id="81ac8-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="81ac8-246">g.</span><span class="sxs-lookup"><span data-stu-id="81ac8-246">g.</span></span> <span data-ttu-id="81ac8-247">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="81ac8-248">![ACEPTAR](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="81ac8-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="81ac8-249">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81ac8-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81ac8-250">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="81ac8-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81ac8-251">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81ac8-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81ac8-252">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="81ac8-253">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81ac8-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="81ac8-255">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="81ac8-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81ac8-256">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81ac8-258">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81ac8-260">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ac8-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81ac8-262">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="81ac8-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81ac8-264">a.</span><span class="sxs-lookup"><span data-stu-id="81ac8-264">a.</span></span> <span data-ttu-id="81ac8-265">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81ac8-266">b.</span><span class="sxs-lookup"><span data-stu-id="81ac8-266">b.</span></span> <span data-ttu-id="81ac8-267">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81ac8-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81ac8-268">c.</span><span class="sxs-lookup"><span data-stu-id="81ac8-268">c.</span></span> <span data-ttu-id="81ac8-269">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81ac8-270">d.</span><span class="sxs-lookup"><span data-stu-id="81ac8-270">d.</span></span> <span data-ttu-id="81ac8-271">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="81ac8-272">Creación de un usuario de prueba de Workday</span><span class="sxs-lookup"><span data-stu-id="81ac8-272">Creating a Workday test user</span></span>

<span data-ttu-id="81ac8-273">Para obtener un usuario de prueba aprovisionado en Workday, deberá ponerse en contacto con el [equipo de soporte técnico de Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="81ac8-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="81ac8-274">El [equipo de soporte técnico de Workday](https://www.workday.com/en-us/partners-services/services/support.html) creará el usuario.</span><span class="sxs-lookup"><span data-stu-id="81ac8-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81ac8-275">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ac8-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81ac8-276">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Workday.</span><span class="sxs-lookup"><span data-stu-id="81ac8-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="81ac8-278">**Para asignar Britta Simon a Workday, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81ac8-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="81ac8-279">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="81ac8-281">En la lista de aplicaciones, seleccione **Workday**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-281">In the applications list, select **Workday**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="81ac8-283">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="81ac8-285">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-285">Click **Add** button.</span></span> <span data-ttu-id="81ac8-286">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="81ac8-288">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="81ac8-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81ac8-289">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81ac8-290">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81ac8-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81ac8-291">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="81ac8-291">Testing single sign-on</span></span>

<span data-ttu-id="81ac8-292">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="81ac8-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="81ac8-293">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81ac8-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81ac8-294">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="81ac8-294">Additional resources</span></span>

* [<span data-ttu-id="81ac8-295">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81ac8-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81ac8-296">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81ac8-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="81ac8-297">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="81ac8-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

