---
title: "Tutorial: Integración de Azure Active Directory con Ceridian Dayforce HCM | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="7cd9b-103">Tutorial: Integración de Azure Active Directory con Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="7cd9b-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="7cd9b-104">En este tutorial, obtendrá información sobre cómo integrar Ceridian Dayforce HCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7cd9b-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cd9b-105">La integración de Ceridian Dayforce HCM con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cd9b-106">En Azure AD puede controlar quién tiene acceso a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="7cd9b-107">Puede permitir que los usuarios inicien sesión automáticamente en Ceridian Dayforce HCM (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7cd9b-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7cd9b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7cd9b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cd9b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cd9b-110">Prerequisites</span></span>

<span data-ttu-id="7cd9b-111">Para configurar la integración de Azure AD con Ceridian Dayforce HCM, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="7cd9b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cd9b-113">Una suscripción habilitada para el inicio de sesión único en Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="7cd9b-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cd9b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cd9b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cd9b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cd9b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cd9b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cd9b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7cd9b-118">Scenario description</span></span>
<span data-ttu-id="7cd9b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cd9b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cd9b-121">Incorporación de Ceridian Dayforce HCM desde la galería</span><span class="sxs-lookup"><span data-stu-id="7cd9b-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="7cd9b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="7cd9b-123">Incorporación de Ceridian Dayforce HCM desde la galería</span><span class="sxs-lookup"><span data-stu-id="7cd9b-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="7cd9b-124">Para configurar la integración de Ceridian Dayforce HCM en Azure AD, es preciso agregar Ceridian Dayforce HCM desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cd9b-125">**Para agregar Ceridian Dayforce HCM desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7cd9b-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cd9b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="7cd9b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cd9b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="7cd9b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="7cd9b-133">En el cuadro de búsqueda, escriba **Ceridian Dayforce HCM**, seleccione **Ceridian Dayforce HCM** en el panel de resultados y después haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM en la lista de resultados](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7cd9b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7cd9b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Ceridian Dayforce HCM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7cd9b-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7cd9b-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Ceridian Dayforce HCM para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="7cd9b-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="7cd9b-139">Para establecer la relación de vínculo, en Ceridian Dayforce HCM, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7cd9b-140">Para configurar y probar el inicio de sesión único de Azure AD con Ceridian Dayforce HCM, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cd9b-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7cd9b-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cd9b-143">**[Crear un usuario de prueba de Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**: para tener un homólogo de Britta Simon en Ceridian Dayforce HCM que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cd9b-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cd9b-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7cd9b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7cd9b-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="7cd9b-148">**Para configurar el inicio de sesión único de Azure AD con Ceridian Dayforce HCM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7cd9b-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7cd9b-149">En Azure Portal, en la página de integración de aplicaciones de **Ceridian Dayforce HCM**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="7cd9b-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="7cd9b-153">En la sección **Dominio y direcciones URL de Ceridian Dayforce HCM**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="7cd9b-155">a.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-155">a.</span></span> <span data-ttu-id="7cd9b-156">En el cuadro de texto **URL de inicio de sesión** , escriba la dirección URL que utilizan los usuarios para iniciar sesión en su aplicación de Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="7cd9b-157">Environment</span><span class="sxs-lookup"><span data-stu-id="7cd9b-157">Environment</span></span> | <span data-ttu-id="7cd9b-158">URL</span><span class="sxs-lookup"><span data-stu-id="7cd9b-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="7cd9b-159">Para producción</span><span class="sxs-lookup"><span data-stu-id="7cd9b-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="7cd9b-160">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="7cd9b-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="7cd9b-161">b.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-161">b.</span></span> <span data-ttu-id="7cd9b-162">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="7cd9b-163">Environment</span><span class="sxs-lookup"><span data-stu-id="7cd9b-163">Environment</span></span> | <span data-ttu-id="7cd9b-164">URL</span><span class="sxs-lookup"><span data-stu-id="7cd9b-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="7cd9b-165">Para producción</span><span class="sxs-lookup"><span data-stu-id="7cd9b-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="7cd9b-166">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="7cd9b-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="7cd9b-167">c.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-167">c.</span></span> <span data-ttu-id="7cd9b-168">En el cuadro de texto **URL de respuesta** , escriba la dirección URL que se usa en Azure AD para exponer la respuesta.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="7cd9b-169">Environment</span><span class="sxs-lookup"><span data-stu-id="7cd9b-169">Environment</span></span> | <span data-ttu-id="7cd9b-170">URL</span><span class="sxs-lookup"><span data-stu-id="7cd9b-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="7cd9b-171">Para producción</span><span class="sxs-lookup"><span data-stu-id="7cd9b-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="7cd9b-172">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="7cd9b-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="7cd9b-173">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-173">These values are not real.</span></span> <span data-ttu-id="7cd9b-174">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="7cd9b-175">Póngase en contacto con el [equipo de soporte de cliente de Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="7cd9b-176">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="7cd9b-178">La aplicación Ceridian Dayforce HCM espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7cd9b-179">Colabore con el [equipo de soporte técnico de Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) para identificar el identificador de usuario correcto.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="7cd9b-180">Microsoft recomienda utilizar el atributo **"name"** como identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="7cd9b-181">Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7cd9b-182">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-182">The following screenshot shows an example for this.</span></span>  

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="7cd9b-184">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="7cd9b-185">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="7cd9b-185">Attribute Name</span></span>  | <span data-ttu-id="7cd9b-186">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="7cd9b-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="7cd9b-187">name</span><span class="sxs-lookup"><span data-stu-id="7cd9b-187">name</span></span>  | <span data-ttu-id="7cd9b-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="7cd9b-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="7cd9b-189">a.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-189">a.</span></span> <span data-ttu-id="7cd9b-190">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7cd9b-193">b.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-193">b.</span></span> <span data-ttu-id="7cd9b-194">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7cd9b-195">c.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-195">c.</span></span> <span data-ttu-id="7cd9b-196">En la lista **Valor** , seleccione el atributo de usuario que desea usar en su implementación.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="7cd9b-197">Por ejemplo, si quiere usar EmployeeID como identificador de usuario único y ha almacenado el valor del atributo en ExtensionAttribute2, seleccione **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="7cd9b-198">d.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-198">d.</span></span> <span data-ttu-id="7cd9b-199">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-199">Click **Ok**.</span></span>

7. <span data-ttu-id="7cd9b-200">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7cd9b-200">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="7cd9b-202">En la sección **Configuración de Ceridian Dayforce HCM**, haga clic en **Configurar Ceridian Dayforce HCM** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7cd9b-203">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="7cd9b-205">Para configurar el inicio de sesión en **Ceridian Dayforce HCM**, necesita enviar el **XML de metadatos** descargado y **la dirección URL de cierre de sesión, el identificador de entidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="7cd9b-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="7cd9b-206">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7cd9b-207">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7cd9b-208">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cd9b-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7cd9b-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-209">Create an Azure AD test user</span></span>

<span data-ttu-id="7cd9b-210">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7cd9b-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="7cd9b-212">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7cd9b-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cd9b-213">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7cd9b-215">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7cd9b-217">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7cd9b-219">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7cd9b-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7cd9b-221">a.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-221">a.</span></span> <span data-ttu-id="7cd9b-222">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cd9b-223">b.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-223">b.</span></span> <span data-ttu-id="7cd9b-224">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7cd9b-225">c.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-225">c.</span></span> <span data-ttu-id="7cd9b-226">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7cd9b-227">d.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-227">d.</span></span> <span data-ttu-id="7cd9b-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="7cd9b-229">Crear un usuario de prueba de Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="7cd9b-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="7cd9b-230">El objetivo de esta sección es crear una usuaria llamada Britta Simon en Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="7cd9b-231">Colabore con el [equipo de soporte técnico de Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) para que agreguen los usuarios a la aplicación de Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7cd9b-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7cd9b-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7cd9b-235">**Para asignar a Britta Simon a Ceridian Dayforce HCM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7cd9b-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7cd9b-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7cd9b-238">En la lista de aplicaciones, seleccione **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="7cd9b-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7cd9b-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-242">Click **Add** button.</span></span> <span data-ttu-id="7cd9b-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7cd9b-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cd9b-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cd9b-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7cd9b-248">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cd9b-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="7cd9b-249">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="7cd9b-251">**Para asignar a Britta Simon a Ceridian Dayforce HCM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7cd9b-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7cd9b-252">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7cd9b-254">En la lista de aplicaciones, seleccione **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Vínculo de Ceridian Dayforce HCM en la lista de aplicaciones](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="7cd9b-256">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="7cd9b-258">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-258">Click **Add** button.</span></span> <span data-ttu-id="7cd9b-259">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="7cd9b-261">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cd9b-262">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cd9b-263">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7cd9b-264">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7cd9b-264">Test single sign-on</span></span>

<span data-ttu-id="7cd9b-265">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7cd9b-266">Al hacer clic en el icono de Ceridian Dayforce HCM en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="7cd9b-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7cd9b-267">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7cd9b-267">Additional resources</span></span>

* [<span data-ttu-id="7cd9b-268">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cd9b-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cd9b-269">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7cd9b-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

