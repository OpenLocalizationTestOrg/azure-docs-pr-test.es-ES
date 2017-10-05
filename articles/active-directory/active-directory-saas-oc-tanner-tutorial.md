---
title: "Tutorial: Integración de Azure Active Directory con O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y O. C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="16216-105">Tutorial: Integración de Azure Active Directory con O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="16216-106">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="16216-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="16216-107">En este tutorial, aprenderá a integrar O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="16216-108">Tanner - AppreciateHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16216-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16216-109">Integración de O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-109">Integrating O.C.</span></span> <span data-ttu-id="16216-110">Tanner - AppreciateHub con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="16216-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16216-111">Puede controlar en Azure AD quién tiene acceso a O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="16216-112">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="16216-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="16216-113">Puede permitir a los usuarios iniciar sesión automáticamente en O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="16216-114">Tanner - AppreciateHub (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16216-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16216-115">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="16216-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16216-116">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16216-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16216-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="16216-117">Prerequisites</span></span>

<span data-ttu-id="16216-118">Para configurar la integración de Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="16216-119">Tanner - AppreciateHub, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="16216-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="16216-120">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-120">An Azure AD subscription</span></span>
- <span data-ttu-id="16216-121">Una suscripción habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="16216-121">A O.C.</span></span> <span data-ttu-id="16216-122">Una suscripción habilitada para el inicio de sesión único en Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="16216-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16216-123">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="16216-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16216-124">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="16216-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16216-125">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="16216-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16216-126">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16216-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16216-127">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="16216-127">Scenario description</span></span>
<span data-ttu-id="16216-128">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="16216-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16216-129">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="16216-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16216-130">Agregar O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-130">Adding O.C.</span></span> <span data-ttu-id="16216-131">Tanner - AppreciateHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="16216-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="16216-132">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="16216-133">Agregar O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-133">Adding O.C.</span></span> <span data-ttu-id="16216-134">Tanner - AppreciateHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="16216-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="16216-135">Para configurar la integración de O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-135">To configure the integration of O.C.</span></span> <span data-ttu-id="16216-136">Tanner - AppreciateHub en Azure AD, debe agregar O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="16216-137">Tanner - AppreciateHub desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="16216-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16216-138">**Para agregar O.C. Tanner - AppreciateHub desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="16216-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16216-139">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16216-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16216-141">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="16216-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16216-142">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="16216-142">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="16216-144">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16216-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="16216-146">En el cuadro de búsqueda, escriba **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="16216-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="16216-148">En el panel de resultados, seleccione **O.C. Tanner - AppreciateHub** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16216-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16216-150">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16216-151">En esta sección, configurará y probará el inicio de sesión único de Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="16216-152">Tanner - AppreciateHub en función de un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="16216-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16216-153">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="16216-154">Tanner - AppreciateHub para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16216-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="16216-155">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de </span><span class="sxs-lookup"><span data-stu-id="16216-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="16216-156">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="16216-157">Para establecer</span><span class="sxs-lookup"><span data-stu-id="16216-157">In O.C.</span></span> <span data-ttu-id="16216-158">la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como el valor de **nombre de usuario** de O.C. Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16216-159">Para configurar y probar el inicio de sesión único en Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="16216-160">Tanner - AppreciateHub, debe completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="16216-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16216-161">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="16216-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16216-162">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16216-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16216-163">**[Creación de un usuario de prueba de O.C. Tanner - AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**: para tener un homólogo de Britta Simon en O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="16216-164">Tanner - AppreciateHub que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16216-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16216-165">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16216-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16216-166">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="16216-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16216-167">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16216-168">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="16216-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="16216-170">**Para configurar y probar el inicio de sesión único en Azure AD con O.C. Tanner - AppreciateHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="16216-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="16216-171">En la página de integración de la aplicación**O.C. Tanner - AppreciateHub**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="16216-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="16216-173">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="16216-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="16216-175">En la sección **Dominio y direcciones URL de O.C. Tanner - AppreciateHub**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="16216-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="16216-177">a.</span><span class="sxs-lookup"><span data-stu-id="16216-177">a.</span></span> <span data-ttu-id="16216-178">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`.</span><span class="sxs-lookup"><span data-stu-id="16216-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16216-179">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="16216-179">This value is not real.</span></span> <span data-ttu-id="16216-180">Actualice este valor con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="16216-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="16216-181">Póngase en contacto con el [equipo de soporte técnico de O.C. Tanner - AppreciateHub](mailto:sso@octanner.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="16216-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="16216-182">b.</span><span class="sxs-lookup"><span data-stu-id="16216-182">b.</span></span> <span data-ttu-id="16216-183">Abra el archivo de metadatos mediante el siguiente vínculo: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="16216-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="16216-184">c.</span><span class="sxs-lookup"><span data-stu-id="16216-184">c.</span></span> <span data-ttu-id="16216-185">Busque el nodo **md:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="16216-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="16216-186">d.</span><span class="sxs-lookup"><span data-stu-id="16216-186">d.</span></span> <span data-ttu-id="16216-187">Copie el valor del atributo **Location** .</span><span class="sxs-lookup"><span data-stu-id="16216-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Configurar las opciones de la aplicación][12]
   
    <span data-ttu-id="16216-189">e.</span><span class="sxs-lookup"><span data-stu-id="16216-189">e.</span></span> <span data-ttu-id="16216-190">En el cuadro de texto **URL de inicio de sesión** , pegue el valor que obtuvo en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="16216-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="16216-191">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="16216-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="16216-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="16216-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16216-195">Para configurar el inicio de sesión único en **O.C. Tanner - AppreciateHub**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de porte técnico de O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="16216-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="16216-196">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16216-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16216-197">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="16216-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16216-198">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16216-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16216-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="16216-200">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="16216-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="16216-202">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="16216-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16216-203">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16216-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16216-205">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="16216-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16216-207">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16216-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16216-209">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="16216-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16216-211">a.</span><span class="sxs-lookup"><span data-stu-id="16216-211">a.</span></span> <span data-ttu-id="16216-212">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16216-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16216-213">b.</span><span class="sxs-lookup"><span data-stu-id="16216-213">b.</span></span> <span data-ttu-id="16216-214">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16216-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16216-215">c.</span><span class="sxs-lookup"><span data-stu-id="16216-215">c.</span></span> <span data-ttu-id="16216-216">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="16216-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16216-217">d.</span><span class="sxs-lookup"><span data-stu-id="16216-217">d.</span></span> <span data-ttu-id="16216-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="16216-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="16216-219">Creación de un usuario de prueba de O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-219">Creating a O.C.</span></span> <span data-ttu-id="16216-220">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="16216-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="16216-221">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="16216-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="16216-223">**Para crear un usuario llamado Simon Britta en O.C. Tanner - AppreciateHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="16216-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="16216-224">Consulte al [equipo de soporte técnico de O.C. Tanner - AppreciateHub](mailto:sso@octanner.com) para crear un usuario que tenga como atributo nameID el mismo valor que el nombre de usuario de Britta Simon en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16216-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16216-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16216-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16216-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="16216-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-227">Tanner - AppreciateHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="16216-229">**Para asignar a Simon Britta a O.C. Tanner - AppreciateHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="16216-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="16216-230">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="16216-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="16216-232">En la lista de aplicaciones, seleccione **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="16216-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="16216-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="16216-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="16216-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="16216-236">Click **Add** button.</span></span> <span data-ttu-id="16216-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="16216-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="16216-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="16216-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16216-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="16216-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16216-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="16216-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16216-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="16216-242">Testing single sign-on</span></span>

<span data-ttu-id="16216-243">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16216-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="16216-244">Cuando hace clic en el icono de O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-244">When you click the O.C.</span></span> <span data-ttu-id="16216-245">Tanner - AppreciateHub en el panel de acceso, debe iniciar sesión automáticamente en la aplicación O.C.</span><span class="sxs-lookup"><span data-stu-id="16216-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="16216-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="16216-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16216-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="16216-247">Additional resources</span></span>

* [<span data-ttu-id="16216-248">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16216-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16216-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16216-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

