---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Public | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="d9c0f-103">Tutorial: Integración de Azure Active Directory con TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="d9c0f-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="d9c0f-104">En este tutorial, obtendrá información sobre cómo integrar TOPdesk - Public con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9c0f-105">La integración de TOPdesk - Public con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9c0f-106">Puede controlar en Azure AD quién tiene acceso a TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="d9c0f-107">Puede permitir que los usuarios inicien sesión automáticamente en TOPdesk - Public (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d9c0f-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d9c0f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9c0f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d9c0f-110">Prerequisites</span></span>

<span data-ttu-id="d9c0f-111">Para configurar la integración de Azure AD con TOPdesk - Public, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="d9c0f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9c0f-113">Una suscripción habilitada para el inicio de sesión único en TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="d9c0f-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9c0f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9c0f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9c0f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9c0f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9c0f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d9c0f-118">Scenario description</span></span>
<span data-ttu-id="d9c0f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9c0f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9c0f-121">Agregar TOPdesk - Public desde la galería</span><span class="sxs-lookup"><span data-stu-id="d9c0f-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="d9c0f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="d9c0f-123">Agregar TOPdesk - Public desde la galería</span><span class="sxs-lookup"><span data-stu-id="d9c0f-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="d9c0f-124">Para configurar la integración de TOPdesk - Public en Azure AD, deberá agregar TOPdesk - Public desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9c0f-125">**Para agregar TOPdesk - Public desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d9c0f-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9c0f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="d9c0f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9c0f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="d9c0f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="d9c0f-133">En el cuadro de búsqueda, escriba **TOPdesk - Public**, seleccione **TOPdesk - Public** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Public en la lista de resultados](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d9c0f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d9c0f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TOPdesk - Public con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d9c0f-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9c0f-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TOPdesk - Public para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="d9c0f-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="d9c0f-139">Para establecer la relación de vínculo, en TOPdesk - Public asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d9c0f-140">Para configurar y probar el inicio de sesión único de Azure AD con TOPdesk - Public, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9c0f-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9c0f-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9c0f-143">**[Creación de un usuario de prueba de TOPdesk - Public](#create-a-topdesk---public-test-user)**: para tener un homólogo de Britta Simon en TOPdesk - Public que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9c0f-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9c0f-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d9c0f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d9c0f-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="d9c0f-148">**Para configurar el inicio de sesión único de Azure AD con TOPdesk - Public, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d9c0f-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="d9c0f-149">En la página de integración de la aplicación **TOPdesk - Public** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="d9c0f-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="d9c0f-153">En la sección **Dominio y direcciones URL de TOPdesk - Public**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="d9c0f-155">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-155">a.</span></span> <span data-ttu-id="d9c0f-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.topdesk.net`.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="d9c0f-157">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-157">b.</span></span> <span data-ttu-id="d9c0f-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="d9c0f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="d9c0f-159">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-159">c.</span></span> <span data-ttu-id="d9c0f-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.topdesk.net/tas/public/login/saml`.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d9c0f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-161">These values are not real.</span></span> <span data-ttu-id="d9c0f-162">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d9c0f-163">La dirección URL de respuesta se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="d9c0f-164">Póngase en contacto con el [equipo de soporte técnico de TOPdesk - Public](https://help.topdesk.com/saas/enterprise/user/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="d9c0f-165">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="d9c0f-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d9c0f-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d9c0f-169">En la sección **TOPdesk - Public Configuration** (Configuración de TOPdesk - Public), haga clic en **Configure TOPdesk - Public** (Configurar TOPdesk - Public) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d9c0f-170">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="d9c0f-172">Inicie sesión en el sitio de la compañía de **TOPdesk - Public** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="d9c0f-173">En el menú **TOPdesk**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="d9c0f-174">![Configuración](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="d9c0f-175">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="d9c0f-176">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="d9c0f-177">Expanda el menú **Login Settings** (Configuración de inicio de sesión) y luego haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="d9c0f-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="d9c0f-179">En la sección **Público** de la sección de configuración **Inicio de sesión SAML**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="d9c0f-180">![Configuración técnica](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configuración técnica")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="d9c0f-181">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-181">a.</span></span> <span data-ttu-id="d9c0f-182">Haga clic en **Download** (Descargar) para descargar el archivo de metadatos público y luego guárdelo localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="d9c0f-183">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-183">b.</span></span> <span data-ttu-id="d9c0f-184">Abra el archivo de metadatos descargado y luego busque el nodo **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="d9c0f-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="d9c0f-186">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-186">c.</span></span> <span data-ttu-id="d9c0f-187">Copia el valor de **AssertionConsumerService**, péguelo en el cuadro de texto **Dirección URL de respuesta** de la sección **Dominio y direcciones URL de TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="d9c0f-188">Lleve a cabo los siguientes pasos para crear un archivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="d9c0f-189">![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="d9c0f-190">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-190">a.</span></span> <span data-ttu-id="d9c0f-191">Abra el archivo de metadatos descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="d9c0f-192">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-192">b.</span></span> <span data-ttu-id="d9c0f-193">Expanda el nodo **RoleDescriptor** cuyo **xsi:type** es **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="d9c0f-194">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-194">c.</span></span> <span data-ttu-id="d9c0f-195">Copie el valor del nodo **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="d9c0f-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="d9c0f-196">d.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-196">d.</span></span> <span data-ttu-id="d9c0f-197">Guarde el valor de **X509Certificate** copiado localmente en el equipo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="d9c0f-198">En la sección **Public** (Público), haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="d9c0f-199">![Inicio de sesión SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Inicio de sesión SAML")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="d9c0f-200">En la página de diálogo del **SAML configuration assistant** (Asistente de configuración de SAML), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="d9c0f-201">![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Asistente de configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="d9c0f-202">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-202">a.</span></span> <span data-ttu-id="d9c0f-203">Para cargar el archivo de metadatos descargado de Azure Portal, en **Federation Metadata** (Metadatos de federación) haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="d9c0f-204">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-204">b.</span></span> <span data-ttu-id="d9c0f-205">Para cargar el archivo del certificado, en **Certificate (RSA)** (Certificado [RSA]), haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="d9c0f-206">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-206">c.</span></span> <span data-ttu-id="d9c0f-207">Para cargar el archivo de logotipo que obtuvo del equipo de soporte técnico de TOPdesk, en **Logo icon** (Icono de logotipo), haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="d9c0f-208">d.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-208">d.</span></span> <span data-ttu-id="d9c0f-209">En el cuadro de texto **User name attribute** (Atributo de nombre de usuario), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="d9c0f-210">e.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-210">e.</span></span> <span data-ttu-id="d9c0f-211">En el cuadro de texto **Display name** (Nombre para mostrar), escriba un nombre para su configuración.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="d9c0f-212">f.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-212">f.</span></span> <span data-ttu-id="d9c0f-213">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d9c0f-214">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9c0f-215">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9c0f-216">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9c0f-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d9c0f-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-217">Create an Azure AD test user</span></span>

<span data-ttu-id="d9c0f-218">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d9c0f-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="d9c0f-220">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d9c0f-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9c0f-221">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d9c0f-223">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d9c0f-225">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d9c0f-227">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-227">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d9c0f-229">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-229">a.</span></span> <span data-ttu-id="d9c0f-230">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9c0f-231">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-231">b.</span></span> <span data-ttu-id="d9c0f-232">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d9c0f-233">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-233">c.</span></span> <span data-ttu-id="d9c0f-234">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d9c0f-235">d.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-235">d.</span></span> <span data-ttu-id="d9c0f-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="d9c0f-237">Creación de un usuario de prueba de TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="d9c0f-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="d9c0f-238">Para permitir que los usuarios de Azure AD inicien sesión en TOPdesk - Public, deben aprovisionarse en TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="d9c0f-239">En el caso de TOPdesk - Public, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="d9c0f-240">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="d9c0f-241">Inicie sesión en su sitio de la compañía de **TOPdesk - Public** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="d9c0f-242">En el menú de la parte superior, haga clic en **TOPdesk \> New \> Support Files \> Person** (TOPdesk > Nuevo > Archivos de soporte > Persona).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="d9c0f-243">![Persona](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Persona")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="d9c0f-244">En el cuadro de diálogo Nueva persona, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d9c0f-245">![Nueva persona](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nueva persona")</span><span class="sxs-lookup"><span data-stu-id="d9c0f-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="d9c0f-246">a.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-246">a.</span></span> <span data-ttu-id="d9c0f-247">Haga clic en la pestaña General.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-247">Click the General tab.</span></span>

    <span data-ttu-id="d9c0f-248">b.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-248">b.</span></span> <span data-ttu-id="d9c0f-249">En el cuadro de texto **Apellidos**, escriba los apellidos del usuario, en este caso, Simon.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="d9c0f-250">c.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-250">c.</span></span> <span data-ttu-id="d9c0f-251">Seleccione un **sitio** para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="d9c0f-252">d.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-252">d.</span></span> <span data-ttu-id="d9c0f-253">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d9c0f-254">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TOPdesk - Public ofrecida por TOPdesk - Public para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d9c0f-255">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9c0f-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="d9c0f-256">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="d9c0f-258">**Para asignar Britta Simon a TOPdesk - Public, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="d9c0f-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="d9c0f-259">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d9c0f-261">En la lista de aplicaciones, seleccione **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![Vínculo a TOPdesk - Public en la lista de aplicaciones](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="d9c0f-263">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-263">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="d9c0f-265">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-265">Click **Add** button.</span></span> <span data-ttu-id="d9c0f-266">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="d9c0f-268">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9c0f-269">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9c0f-270">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d9c0f-271">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d9c0f-271">Test single sign-on</span></span>

<span data-ttu-id="d9c0f-272">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d9c0f-273">Al hacer clic en el icono de TOPdesk - Public en el panel de acceso, debería iniciar sesión automáticamente en la aplicación TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="d9c0f-274">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9c0f-275">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d9c0f-275">Additional resources</span></span>

* [<span data-ttu-id="d9c0f-276">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9c0f-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9c0f-277">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9c0f-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

