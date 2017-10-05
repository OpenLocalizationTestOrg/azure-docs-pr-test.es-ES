---
title: "Tutorial: integración de Azure Active Directory con Syncplicity | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="52232-103">Tutorial: integración de Azure Active Directory con Syncplicity</span><span class="sxs-lookup"><span data-stu-id="52232-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="52232-104">En este tutorial, aprenderá a integrar Syncplicity con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52232-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52232-105">La integración de Syncplicity con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="52232-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52232-106">Puede controlar en Azure AD quién tiene acceso a Syncplicity</span><span class="sxs-lookup"><span data-stu-id="52232-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="52232-107">Puede habilitar que los usuarios inicien sesión automáticamente en Syncplicity (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52232-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52232-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="52232-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52232-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52232-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52232-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52232-110">Prerequisites</span></span>

<span data-ttu-id="52232-111">Para configurar la integración de Azure AD con Syncplicity, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="52232-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="52232-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52232-113">Una suscripción habilitada para el inicio de sesión único en Syncplicity</span><span class="sxs-lookup"><span data-stu-id="52232-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52232-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="52232-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52232-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="52232-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52232-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="52232-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52232-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52232-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52232-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="52232-118">Scenario description</span></span>
<span data-ttu-id="52232-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="52232-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52232-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="52232-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52232-121">Incorporación de Syncplicity desde la galería</span><span class="sxs-lookup"><span data-stu-id="52232-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="52232-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="52232-123">Incorporación de Syncplicity desde la galería</span><span class="sxs-lookup"><span data-stu-id="52232-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="52232-124">Para configurar la integración de Syncplicity en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="52232-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52232-125">**Para agregar Syncplicity desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52232-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52232-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52232-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52232-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="52232-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52232-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52232-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="52232-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52232-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="52232-133">En el cuadro de búsqueda, escriba **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="52232-133">In the search box, type **Syncplicity**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="52232-135">En el panel de resultados, seleccione **Syncplicity** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52232-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52232-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52232-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Syncplicity con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52232-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52232-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Syncplicity para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52232-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="52232-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="52232-141">Para establecer la relación de vínculo, en Syncplicity, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="52232-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52232-142">Para configurar y probar el inicio de sesión único de Azure AD con Syncplicity, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="52232-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52232-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="52232-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52232-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52232-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52232-145">**[Creación de un usuario de prueba de Syncplicity](#creating-a-syncplicity-test-user)**: para tener un homólogo de Britta Simon en Syncplicity vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52232-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52232-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52232-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52232-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="52232-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52232-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52232-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="52232-150">**Para configurar el inicio de sesión único de Azure AD con Syncplicity, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52232-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="52232-151">En Azure Portal, en la página de integración de la aplicación **Syncplicity**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="52232-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="52232-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52232-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="52232-155">En la sección **Syncplicity Domain and URLs** (Dominio y direcciones URL de Syncplicity), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="52232-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="52232-157">a.</span><span class="sxs-lookup"><span data-stu-id="52232-157">a.</span></span> <span data-ttu-id="52232-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.syncplicity.com`.</span><span class="sxs-lookup"><span data-stu-id="52232-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="52232-159">b.</span><span class="sxs-lookup"><span data-stu-id="52232-159">b.</span></span> <span data-ttu-id="52232-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="52232-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52232-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="52232-161">These values are not real.</span></span> <span data-ttu-id="52232-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="52232-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52232-163">Póngase en contacto con el [equipo de soporte de cliente de Syncplicity](https://www.syncplicity.com/contact-us) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="52232-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="52232-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52232-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="52232-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="52232-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52232-168">En la sección **Syncplicity Configuration** (Configuración de Syncplicity), haga clic en **Configure Syncplicity** (Configurar Syncplicity) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="52232-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="52232-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="52232-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="52232-171">Inicie sesión en su inquilino de **Syncplicity** .</span><span class="sxs-lookup"><span data-stu-id="52232-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="52232-172">En el menú en la parte superior, haga clic en **admin** (Administración), seleccione **settings** (Configuración) y luego haga clic en **Custom domain and single sign-on** (Dominio personalizado e inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="52232-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="52232-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="52232-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="52232-174">En la página del cuadro de diálogo **Single Sign-On (SSO)** (Configuración de inicio de sesión único [SSO]), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="52232-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="52232-175">![Inicio de sesión único \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="52232-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="52232-176">a.</span><span class="sxs-lookup"><span data-stu-id="52232-176">a.</span></span> <span data-ttu-id="52232-177">En el cuadro de texto **Custom Domain** (Dominio personalizado), escriba el nombre de su dominio.</span><span class="sxs-lookup"><span data-stu-id="52232-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="52232-178">b.</span><span class="sxs-lookup"><span data-stu-id="52232-178">b.</span></span> <span data-ttu-id="52232-179">Seleccione **Enabled** (Habilitado) como **Single Sign-On Status** (Estado de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="52232-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="52232-180">c.</span><span class="sxs-lookup"><span data-stu-id="52232-180">c.</span></span> <span data-ttu-id="52232-181">En el cuadro de texto **Id. de entidad**, pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="52232-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="52232-182">d.</span><span class="sxs-lookup"><span data-stu-id="52232-182">d.</span></span> <span data-ttu-id="52232-183">Copie el valor de **SAML Single Sign-On Service URL** (Dirección URL de inicio de sesión único de SAML) que ha copiado de Azure Portal en el cuadro de texto **Sign-in page URL** (Dirección URL de la página de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="52232-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="52232-184">e.</span><span class="sxs-lookup"><span data-stu-id="52232-184">e.</span></span> <span data-ttu-id="52232-185">Copie el valor de **Sign-out URL** (Dirección URL de cierre de sesión) que ha copiado de Azure Portal en el cuadro de texto **Logout page URL** (Dirección URL de la página de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="52232-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="52232-186">f.</span><span class="sxs-lookup"><span data-stu-id="52232-186">f.</span></span> <span data-ttu-id="52232-187">En **Identity Provider Certificate** (Certificado del proveedor de identidades), haga clic en **Elegir archivo** y cargue el certificado que ha descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="52232-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="52232-188">g.</span><span class="sxs-lookup"><span data-stu-id="52232-188">g.</span></span> <span data-ttu-id="52232-189">Haga clic en **GURDAR CAMBIOS**.</span><span class="sxs-lookup"><span data-stu-id="52232-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="52232-190">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52232-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52232-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="52232-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52232-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52232-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52232-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="52232-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52232-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="52232-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="52232-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52232-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52232-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52232-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="52232-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52232-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52232-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52232-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="52232-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52232-205">a.</span><span class="sxs-lookup"><span data-stu-id="52232-205">a.</span></span> <span data-ttu-id="52232-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52232-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52232-207">b.</span><span class="sxs-lookup"><span data-stu-id="52232-207">b.</span></span> <span data-ttu-id="52232-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52232-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52232-209">c.</span><span class="sxs-lookup"><span data-stu-id="52232-209">c.</span></span> <span data-ttu-id="52232-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="52232-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52232-211">d.</span><span class="sxs-lookup"><span data-stu-id="52232-211">d.</span></span> <span data-ttu-id="52232-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="52232-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="52232-213">Creación de un usuario de prueba de Syncplicity</span><span class="sxs-lookup"><span data-stu-id="52232-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="52232-214">Para que los usuarios de AAD puedan iniciar sesión, deben aprovisionarse a Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="52232-215">En esta sección se describe cómo crear cuentas de usuario de AAD en Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="52232-216">**Para aprovisionar cuentas de usuario en Syncplicity, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="52232-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="52232-217">Inicie sesión en su inquilino de **Syncplicity** (por ejemplo, `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="52232-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="52232-218">Haga clic en **admin** y seleccione **cuentas de usuario**.</span><span class="sxs-lookup"><span data-stu-id="52232-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="52232-219">Haga clic en **ADD A USER** (AGREGAR UN USUARIO).</span><span class="sxs-lookup"><span data-stu-id="52232-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="52232-220">![Administración de usuarios](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="52232-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="52232-221">Escriba las **Email Address** (Direcciones de correo electrónico) de una cuenta de AAD que quiera aprovisionar, seleccione **User** (Usuario) como **Role** (Rol) y haga clic en **NEXT** (SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="52232-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="52232-222">![Información de la cuenta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Información de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="52232-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="52232-223">El titular de la cuenta de AAD recibirá un mensaje de correo electrónico junto con un vínculo para confirmar y activar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="52232-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="52232-224">Seleccione un grupo de la compañía de la que debe convertirse en miembro su nuevo usuario y haga clic en **NEXT**(SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="52232-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="52232-225">![Pertenencia a grupos](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Pertenencia a grupos")</span><span class="sxs-lookup"><span data-stu-id="52232-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="52232-226">Si no se muestra ningún grupo, haga clic en **NEXT**(SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="52232-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="52232-227">Seleccione las carpetas que desea colocar bajo el control de Syncplicity en el equipo del usuario y haga clic en **NEXT**(SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="52232-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="52232-228">![Carpetas de Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Carpetas de Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="52232-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="52232-229">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Syncplicity ofrecida por Syncplicity para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="52232-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52232-230">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52232-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52232-231">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="52232-233">**Para asignar Britta Simon a Syncplicity, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52232-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="52232-234">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52232-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="52232-236">En la lista de aplicaciones, seleccione **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="52232-236">In the applications list, select **Syncplicity**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="52232-238">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52232-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="52232-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="52232-240">Click **Add** button.</span></span> <span data-ttu-id="52232-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52232-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="52232-243">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="52232-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52232-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52232-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52232-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52232-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52232-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="52232-246">Testing single sign-on</span></span>

<span data-ttu-id="52232-247">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="52232-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52232-248">Al hacer clic en el icono de Syncplicity en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="52232-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="52232-249">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="52232-249">Additional resources</span></span>

* [<span data-ttu-id="52232-250">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52232-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52232-251">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52232-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

