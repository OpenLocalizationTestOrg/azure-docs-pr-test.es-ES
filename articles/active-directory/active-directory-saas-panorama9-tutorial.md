---
title: "Tutorial: Integración de Azure Active Directory con Panorama9 | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="3f3d3-103">Tutorial: Integración de Azure Active Directory con Panorama9</span><span class="sxs-lookup"><span data-stu-id="3f3d3-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="3f3d3-104">En este tutorial, aprenderá a integrar Panorama9 con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f3d3-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f3d3-105">La integración de Panorama9 con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f3d3-106">Puede controlar en Azure AD quién tiene acceso a Panorama9</span><span class="sxs-lookup"><span data-stu-id="3f3d3-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="3f3d3-107">Puede permitir que los usuarios inicien sesión automáticamente en Panorama9 (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f3d3-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f3d3-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f3d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f3d3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3f3d3-110">Prerequisites</span></span>

<span data-ttu-id="3f3d3-111">Para configurar la integración de Azure AD con Panorama9, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="3f3d3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f3d3-113">Una suscripción habilitada para el inicio de sesión único en Panorama9</span><span class="sxs-lookup"><span data-stu-id="3f3d3-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f3d3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f3d3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f3d3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f3d3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f3d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f3d3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3f3d3-118">Scenario description</span></span>
<span data-ttu-id="3f3d3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f3d3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f3d3-121">Agregación de Panorama9 desde la galería</span><span class="sxs-lookup"><span data-stu-id="3f3d3-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="3f3d3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="3f3d3-123">Agregación de Panorama9 desde la galería</span><span class="sxs-lookup"><span data-stu-id="3f3d3-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="3f3d3-124">Para configurar la integración de Panorama9 en Azure AD, será preciso que agregue Panorama9 desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f3d3-125">**Para agregar Panorama9 desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f3d3-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f3d3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f3d3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f3d3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3f3d3-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3f3d3-133">En el cuadro de búsqueda, escriba **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-133">In the search box, type **Panorama9**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="3f3d3-135">En el panel de resultados, seleccione **Panorama9** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f3d3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3f3d3-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Panorama9 con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3f3d3-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f3d3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Panorama9 para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="3f3d3-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Panorama9.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="3f3d3-141">Para establecer la relación de vínculo, en Panorama9, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3f3d3-142">Para configurar y probar el inicio de sesión único de Azure AD con Panorama9, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f3d3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f3d3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f3d3-145">**[Creación de un usuario de prueba de Panorama9](#creating-a-panorama9-test-user)**: el objetivo es tener un homólogo de Britta Simon en Panorama9 que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f3d3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f3d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f3d3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f3d3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Panorama9.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="3f3d3-150">**Para configurar el inicio de sesión único de Azure AD con Panorama9, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f3d3-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="3f3d3-151">En Azure Portal, en la página de integración de la aplicación **Panorama9**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3f3d3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="3f3d3-155">En la sección **Dominio y direcciones URL de Panorama9**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="3f3d3-157">a.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-157">a.</span></span> <span data-ttu-id="3f3d3-158">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="3f3d3-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="3f3d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-159">b.</span></span> <span data-ttu-id="3f3d3-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="3f3d3-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f3d3-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-161">These values are not real.</span></span> <span data-ttu-id="3f3d3-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3f3d3-163">Póngase en contacto con el [equipo de soporte técnico de Panorama9](https://support.panorama9.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="3f3d3-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="3f3d3-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3f3d3-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f3d3-168">En la sección **Configuración de Panorama9**, haga clic en **Configurar Panorama9** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3f3d3-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="3f3d3-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía Panorama9 como administrador.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="3f3d3-172">En la barra de herramientas de la parte superior, haga clic en **Administrar** y luego en **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="3f3d3-173">![Extensiones](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensiones")</span><span class="sxs-lookup"><span data-stu-id="3f3d3-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="3f3d3-174">En el diálogo **Extensiones**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="3f3d3-175">![Inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="3f3d3-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="3f3d3-176">En la sección **Configuración** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="3f3d3-177">![Configuración](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="3f3d3-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="3f3d3-178">a.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-178">a.</span></span> <span data-ttu-id="3f3d3-179">En el cuadro de texto **Identity Provider URL** (Dirección URL del proveedor de identidades), pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que ha copiado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3f3d3-180">b.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-180">b.</span></span> <span data-ttu-id="3f3d3-181">En el cuadro de texto **Certificate Fingerprint** (Huella digital de certificado), pegue el valor de **Huella digital** del certificado que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="3f3d3-182">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3f3d3-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f3d3-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f3d3-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f3d3-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f3d3-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f3d3-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3f3d3-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3f3d3-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3f3d3-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f3d3-190">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f3d3-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f3d3-194">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f3d3-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3f3d3-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f3d3-198">a.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-198">a.</span></span> <span data-ttu-id="3f3d3-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f3d3-200">b.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-200">b.</span></span> <span data-ttu-id="3f3d3-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f3d3-202">c.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-202">c.</span></span> <span data-ttu-id="3f3d3-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f3d3-204">d.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-204">d.</span></span> <span data-ttu-id="3f3d3-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="3f3d3-206">Creación de un usuario de prueba de Panorama9</span><span class="sxs-lookup"><span data-stu-id="3f3d3-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="3f3d3-207">Para permitir que los usuarios de Azure AD inicien sesión en Panorama9, deben aprovisionarse en Panorama9.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="3f3d3-208">En el caso de Panorama9, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="3f3d3-209">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="3f3d3-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3f3d3-210">Inicie sesión en el sitio de la compañía **Panorama9** como administrador.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="3f3d3-211">En el menú en la parte superior, haga clic en **Administrar** y luego haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="3f3d3-212">![Usuarios](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="3f3d3-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="3f3d3-213">En la sección Usuarios, haga clic en  **+**  para agregar un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="3f3d3-214">![Usuarios](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="3f3d3-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="3f3d3-215">Vaya a la sección Datos de usuario y escriba la dirección de correo electrónico de un usuario válido de Azure Active Directory que desee aprovisionar en el cuadro de texto **Correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="3f3d3-216">En la sección Usuarios, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="3f3d3-217">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f3d3-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3d3-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f3d3-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Panorama9.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3f3d3-221">**Para asignar a Britta Simon a Panorama9, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f3d3-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="3f3d3-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3f3d3-224">En la lista de aplicaciones, seleccione **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-224">In the applications list, select **Panorama9**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="3f3d3-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3f3d3-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-228">Click **Add** button.</span></span> <span data-ttu-id="3f3d3-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3f3d3-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f3d3-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f3d3-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f3d3-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3f3d3-234">Testing single sign-on</span></span>

<span data-ttu-id="3f3d3-235">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f3d3-236">Al hacer clic en el icono de Panorama9 en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Panorama9.</span><span class="sxs-lookup"><span data-stu-id="3f3d3-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="3f3d3-237">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f3d3-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f3d3-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3f3d3-238">Additional resources</span></span>

* [<span data-ttu-id="3f3d3-239">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f3d3-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f3d3-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f3d3-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

