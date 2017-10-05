---
title: "Tutorial: integración de Azure Active Directory con AppDynamics | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="babd5-103">Tutorial: Integración de Azure Active Directory con AppDynamics</span><span class="sxs-lookup"><span data-stu-id="babd5-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="babd5-104">En este tutorial, obtendrá información sobre cómo integrar AppDynamics con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="babd5-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="babd5-105">La integración de AppDynamics con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="babd5-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="babd5-106">En Azure AD puede controlar quién tiene acceso a AppDynamics</span><span class="sxs-lookup"><span data-stu-id="babd5-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="babd5-107">Puede permitir que los usuarios inicien sesión automáticamente en AppDynamics (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="babd5-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="babd5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="babd5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="babd5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="babd5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="babd5-110">Prerequisites</span></span>

<span data-ttu-id="babd5-111">Para configurar la integración de Azure AD con AppDynamics, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="babd5-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="babd5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="babd5-113">Una suscripción habilitada para el inicio de sesión único en AppDynamics</span><span class="sxs-lookup"><span data-stu-id="babd5-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="babd5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="babd5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="babd5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="babd5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="babd5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="babd5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="babd5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="babd5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="babd5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="babd5-118">Scenario description</span></span>
<span data-ttu-id="babd5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="babd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="babd5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="babd5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="babd5-121">Incorporación de AppDynamics desde la galería</span><span class="sxs-lookup"><span data-stu-id="babd5-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="babd5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="babd5-123">Incorporación de AppDynamics desde la galería</span><span class="sxs-lookup"><span data-stu-id="babd5-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="babd5-124">Para configurar la integración de AppDynamics en Azure AD, será preciso que agregue AppDynamics desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="babd5-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="babd5-125">**Para agregar AppDynamics desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="babd5-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="babd5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="babd5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="babd5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="babd5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="babd5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="babd5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="babd5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="babd5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="babd5-133">En el cuadro de búsqueda, escriba **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="babd5-133">In the search box, type **AppDynamics**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="babd5-135">En el panel de resultados, seleccione **AppDynamics** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="babd5-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="babd5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="babd5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AppDynamics con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="babd5-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="babd5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de AppDynamics para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="babd5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="babd5-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="babd5-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="babd5-141">Para establecer la relación de vínculo, en AppDynamics, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="babd5-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="babd5-142">Para configurar y probar el inicio de sesión único de Azure AD con AppDynamics, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="babd5-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="babd5-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="babd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="babd5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="babd5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="babd5-145">**[Creación de un usuario de prueba de AppDynamics](#creating-an-appdynamics-test-user)**: para tener un homólogo de Britta Simon en AppDynamics que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="babd5-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="babd5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="babd5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="babd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="babd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="babd5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="babd5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="babd5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="babd5-150">**Para configurar el inicio de sesión único de Azure AD con AppDynamics, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="babd5-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="babd5-151">En Azure Portal, en la página de integración de la aplicación **AppDynamics**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="babd5-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="babd5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="babd5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="babd5-155">En la sección de **dominio y direcciones URL de AppDynamics**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="babd5-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="babd5-157">a.</span><span class="sxs-lookup"><span data-stu-id="babd5-157">a.</span></span> <span data-ttu-id="babd5-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.saas.appdynamics.com`.</span><span class="sxs-lookup"><span data-stu-id="babd5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="babd5-159">b.</span><span class="sxs-lookup"><span data-stu-id="babd5-159">b.</span></span> <span data-ttu-id="babd5-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="babd5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="babd5-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="babd5-161">These values are not real.</span></span> <span data-ttu-id="babd5-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="babd5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="babd5-163">Póngase en contacto con el [equipo de soporte técnico de cliente de AppDynamics](https://www.appdynamics.com/support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="babd5-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="babd5-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="babd5-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="babd5-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="babd5-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="babd5-168">En la sección **Configuración de AppDynamics**, haga clic en **Configurar AppDynamics** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="babd5-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="babd5-169">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="babd5-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="babd5-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de AppDynamics como administrador.</span><span class="sxs-lookup"><span data-stu-id="babd5-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="babd5-172">En la barra de herramientas de la parte superior, haga clic en **Configuración** y luego en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="babd5-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="babd5-173">![Administración](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="babd5-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="babd5-174">Haga clic en la pestaña **Authentication Provider** (Proveedor de autenticación).</span><span class="sxs-lookup"><span data-stu-id="babd5-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="babd5-175">![Proveedor de autenticación](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Proveedor de autenticación")</span><span class="sxs-lookup"><span data-stu-id="babd5-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="babd5-176">En la sección **Proveedor de autenticación** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="babd5-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="babd5-177">![Configuración de SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="babd5-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="babd5-178">a.</span><span class="sxs-lookup"><span data-stu-id="babd5-178">a.</span></span> <span data-ttu-id="babd5-179">En **Authentication Provider** (Proveedor de autenticación), seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="babd5-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="babd5-180">b.</span><span class="sxs-lookup"><span data-stu-id="babd5-180">b.</span></span> <span data-ttu-id="babd5-181">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="babd5-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="babd5-182">c.</span><span class="sxs-lookup"><span data-stu-id="babd5-182">c.</span></span> <span data-ttu-id="babd5-183">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="babd5-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="babd5-184">d.</span><span class="sxs-lookup"><span data-stu-id="babd5-184">d.</span></span> <span data-ttu-id="babd5-185">Abra el certificado codificado en base 64 en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="babd5-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="babd5-186">e.</span><span class="sxs-lookup"><span data-stu-id="babd5-186">e.</span></span> <span data-ttu-id="babd5-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="babd5-187">Click **Save**.</span></span>

     <span data-ttu-id="babd5-188">![Guardar](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Guardar")</span><span class="sxs-lookup"><span data-stu-id="babd5-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="babd5-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="babd5-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="babd5-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="babd5-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="babd5-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="babd5-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="babd5-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="babd5-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="babd5-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="babd5-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="babd5-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="babd5-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="babd5-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="babd5-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="babd5-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="babd5-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="babd5-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="babd5-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="babd5-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="babd5-204">a.</span><span class="sxs-lookup"><span data-stu-id="babd5-204">a.</span></span> <span data-ttu-id="babd5-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="babd5-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="babd5-206">b.</span><span class="sxs-lookup"><span data-stu-id="babd5-206">b.</span></span> <span data-ttu-id="babd5-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="babd5-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="babd5-208">c.</span><span class="sxs-lookup"><span data-stu-id="babd5-208">c.</span></span> <span data-ttu-id="babd5-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="babd5-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="babd5-210">d.</span><span class="sxs-lookup"><span data-stu-id="babd5-210">d.</span></span> <span data-ttu-id="babd5-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="babd5-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="babd5-212">Creación de un usuario de prueba de AppDynamics</span><span class="sxs-lookup"><span data-stu-id="babd5-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="babd5-213">Para permitir que los usuarios de Azure AD inicien sesión en AppDynamics, tienen que aprovisionarse en AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="babd5-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="babd5-214">En el caso de AppDynamics, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="babd5-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="babd5-215">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="babd5-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="babd5-216">Inicie sesión en su sitio de la compañía de AppDynamics como administrador.</span><span class="sxs-lookup"><span data-stu-id="babd5-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="babd5-217">Vaya a **Users** (Usuarios) y, a continuación, haga clic en **+** para abrir el cuadro de diálogo **Create User** (Crear usuario).</span><span class="sxs-lookup"><span data-stu-id="babd5-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="babd5-218">![Usuarios](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="babd5-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="babd5-219">En la sección **Crear usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="babd5-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="babd5-220">![Creación de usuarios](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="babd5-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="babd5-221">a.</span><span class="sxs-lookup"><span data-stu-id="babd5-221">a.</span></span> <span data-ttu-id="babd5-222">Escriba **Nombre de usuario**, **Nombre**, **Correo electrónico**, **Nueva contraseña**, **Repetir nueva contraseña** de una cuenta válida de AAD que desee aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="babd5-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="babd5-223">b.</span><span class="sxs-lookup"><span data-stu-id="babd5-223">b.</span></span> <span data-ttu-id="babd5-224">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="babd5-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="babd5-225">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de AppDynamics suministrada por AppDynamics para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="babd5-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="babd5-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="babd5-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="babd5-227">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="babd5-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="babd5-229">**Para asignar Britta Simon a AppDynamics, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="babd5-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="babd5-230">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="babd5-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="babd5-232">En la lista de aplicaciones, seleccione **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="babd5-232">In the applications list, select **AppDynamics**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="babd5-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="babd5-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="babd5-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="babd5-236">Click **Add** button.</span></span> <span data-ttu-id="babd5-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="babd5-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="babd5-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="babd5-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="babd5-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="babd5-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="babd5-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="babd5-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="babd5-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="babd5-242">Testing single sign-on</span></span>

<span data-ttu-id="babd5-243">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="babd5-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="babd5-244">Al hacer clic en el icono de AppDynamics en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="babd5-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="babd5-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="babd5-245">Additional resources</span></span>

* [<span data-ttu-id="babd5-246">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="babd5-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="babd5-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="babd5-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

