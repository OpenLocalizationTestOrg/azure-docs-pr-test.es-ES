---
title: "Tutorial: Integración de Azure Active Directory con xMatters OnDemand | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="28eb5-103">Tutorial: Integración de Azure Active Directory con xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="28eb5-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="28eb5-104">En este tutorial, aprenderá a integrar xMatters OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28eb5-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28eb5-105">Integrar xMatters OnDemand con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="28eb5-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="28eb5-106">Puede controlar en Azure AD quién tiene acceso a xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="28eb5-107">Puede permitir que los usuarios inicien sesión automáticamente en xMatters OnDemand (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28eb5-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28eb5-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="28eb5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="28eb5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28eb5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28eb5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="28eb5-110">Prerequisites</span></span>

<span data-ttu-id="28eb5-111">Para configurar la integración de Azure AD con xMatters OnDemand, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="28eb5-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="28eb5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28eb5-113">Una suscripción habilitada para el inicio de sesión único en xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="28eb5-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28eb5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="28eb5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28eb5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="28eb5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28eb5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="28eb5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28eb5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28eb5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28eb5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="28eb5-118">Scenario description</span></span>
<span data-ttu-id="28eb5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="28eb5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28eb5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="28eb5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28eb5-121">Incorporación de xMatters OnDemand desde la galería</span><span class="sxs-lookup"><span data-stu-id="28eb5-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="28eb5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="28eb5-123">Incorporación de xMatters OnDemand desde la galería</span><span class="sxs-lookup"><span data-stu-id="28eb5-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="28eb5-124">Para configurar la integración de xMatters OnDemand en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="28eb5-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28eb5-125">**Para agregar xMatters OnDemand desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="28eb5-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28eb5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28eb5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="28eb5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="28eb5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28eb5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="28eb5-133">En el cuadro de búsqueda, escriba **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="28eb5-135">En el panel de resultados, seleccione **xMatters OnDemand** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28eb5-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28eb5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28eb5-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28eb5-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28eb5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de xMatters OnDemand para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28eb5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="28eb5-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="28eb5-141">Para establecer la relación de vínculo, en xMatters OnDemand, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="28eb5-142">Para configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="28eb5-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28eb5-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="28eb5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28eb5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28eb5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28eb5-145">**[Creación de un usuario de prueba de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**: para tener un homólogo de Britta Simon en xMatters OnDemand que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="28eb5-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="28eb5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28eb5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28eb5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="28eb5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28eb5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28eb5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="28eb5-150">**Para configurar el inicio de sesión único de Azure AD con xMatters OnDemand, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="28eb5-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="28eb5-151">En Azure Portal, en la página de integración de la aplicación **xMatters OnDemand**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="28eb5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="28eb5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="28eb5-155">En la sección **Dominio y direcciones URL de xMatters OnDemand**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="28eb5-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="28eb5-157">a.</span><span class="sxs-lookup"><span data-stu-id="28eb5-157">a.</span></span> <span data-ttu-id="28eb5-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="28eb5-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="28eb5-159">b.</span><span class="sxs-lookup"><span data-stu-id="28eb5-159">b.</span></span> <span data-ttu-id="28eb5-160">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="28eb5-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="28eb5-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="28eb5-161">These values are not real.</span></span> <span data-ttu-id="28eb5-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="28eb5-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="28eb5-163">Póngase en contacto con el [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="28eb5-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="28eb5-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado localmente en **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="28eb5-166">Debe reenviar el certificado al [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="28eb5-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="28eb5-167">El equipo de soporte técnico de xMatters debe cargar el certificado para que se pueda finalizar la configuración del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="28eb5-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="28eb5-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="28eb5-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="28eb5-170">En la sección **Configuración de xMatters OnDemand**, haga clic en **Configurar xMatters OnDemand** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="28eb5-171">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="28eb5-173">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de xMatters OnDemand como administrador.</span><span class="sxs-lookup"><span data-stu-id="28eb5-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="28eb5-174">En la barra de herramientas de la parte superior, haga clic en **Administrador** y luego en **Detalles de la compañía** en la barra de navegación del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="28eb5-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="28eb5-175">![Administración](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="28eb5-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="28eb5-176">En la página **Configuración de SAML** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="28eb5-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="28eb5-177">![Configuración de SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="28eb5-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="28eb5-178">a.</span><span class="sxs-lookup"><span data-stu-id="28eb5-178">a.</span></span> <span data-ttu-id="28eb5-179">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="28eb5-180">b.</span><span class="sxs-lookup"><span data-stu-id="28eb5-180">b.</span></span> <span data-ttu-id="28eb5-181">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **Id. de proveedor de identidad**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="28eb5-182">c.</span><span class="sxs-lookup"><span data-stu-id="28eb5-182">c.</span></span> <span data-ttu-id="28eb5-183">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL de publicación de SAML) que copió de Azure Portal en el cuadro de texto **Dirección URL de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="28eb5-184">d.</span><span class="sxs-lookup"><span data-stu-id="28eb5-184">d.</span></span> <span data-ttu-id="28eb5-185">Pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal en el cuadro de texto **Dirección URL de cierre de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="28eb5-186">e.</span><span class="sxs-lookup"><span data-stu-id="28eb5-186">e.</span></span> <span data-ttu-id="28eb5-187">En la página de detalles de la compañía, en la parte superior, haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="28eb5-188">![Detalles de la compañía](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Detalles de la compañía")</span><span class="sxs-lookup"><span data-stu-id="28eb5-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="28eb5-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28eb5-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="28eb5-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="28eb5-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="28eb5-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28eb5-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28eb5-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="28eb5-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28eb5-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="28eb5-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="28eb5-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28eb5-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28eb5-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28eb5-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28eb5-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28eb5-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="28eb5-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28eb5-204">a.</span><span class="sxs-lookup"><span data-stu-id="28eb5-204">a.</span></span> <span data-ttu-id="28eb5-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28eb5-206">b.</span><span class="sxs-lookup"><span data-stu-id="28eb5-206">b.</span></span> <span data-ttu-id="28eb5-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28eb5-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28eb5-208">c.</span><span class="sxs-lookup"><span data-stu-id="28eb5-208">c.</span></span> <span data-ttu-id="28eb5-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="28eb5-210">d.</span><span class="sxs-lookup"><span data-stu-id="28eb5-210">d.</span></span> <span data-ttu-id="28eb5-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="28eb5-212">Creación de un usuario de prueba de xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="28eb5-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="28eb5-213">Para permitir que los usuarios de Azure AD inicien sesión en xMatters OnDemand, deben aprovisionarse a XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="28eb5-214">En el caso de XMatters OnDemand, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="28eb5-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="28eb5-215">Para aprovisionar cuentas de usuario, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="28eb5-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="28eb5-216">Inicie sesión en su inquilino de **xMatters OnDemand** .</span><span class="sxs-lookup"><span data-stu-id="28eb5-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="28eb5-217">Haga clic en la pestaña **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="28eb5-217">Click **Users** tab.</span></span> <span data-ttu-id="28eb5-218">y, luego, en **Add User** (Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="28eb5-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="28eb5-219">![Usuarios](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="28eb5-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="28eb5-220">En la sección **Agregar un usuario** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="28eb5-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="28eb5-221">![Agregar un usuario](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Agregar un usuario")</span><span class="sxs-lookup"><span data-stu-id="28eb5-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="28eb5-222">a.</span><span class="sxs-lookup"><span data-stu-id="28eb5-222">a.</span></span> <span data-ttu-id="28eb5-223">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="28eb5-223">Select **Active**.</span></span>

    <span data-ttu-id="28eb5-224">b.</span><span class="sxs-lookup"><span data-stu-id="28eb5-224">b.</span></span> <span data-ttu-id="28eb5-225">En el cuadro de texto **User ID** (Identificador de usuario), escriba el identificador de usuario, en este caso, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="28eb5-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="28eb5-226">c.</span><span class="sxs-lookup"><span data-stu-id="28eb5-226">c.</span></span> <span data-ttu-id="28eb5-227">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, Britta.</span><span class="sxs-lookup"><span data-stu-id="28eb5-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="28eb5-228">d.</span><span class="sxs-lookup"><span data-stu-id="28eb5-228">d.</span></span> <span data-ttu-id="28eb5-229">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso Simon.</span><span class="sxs-lookup"><span data-stu-id="28eb5-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="28eb5-230">e.</span><span class="sxs-lookup"><span data-stu-id="28eb5-230">e.</span></span> <span data-ttu-id="28eb5-231">En el cuadro de texto **Sitio**, escriba el sitio válido de una cuenta de Azure AD válida que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="28eb5-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="28eb5-232">f.</span><span class="sxs-lookup"><span data-stu-id="28eb5-232">f.</span></span> <span data-ttu-id="28eb5-233">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="28eb5-234">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28eb5-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="28eb5-235">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="28eb5-237">**Para asignar a Britta Simon a xMatters OnDemand, lleve a cabo los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="28eb5-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="28eb5-238">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="28eb5-240">En la lista de aplicaciones, seleccione  **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="28eb5-242">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="28eb5-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-244">Click **Add** button.</span></span> <span data-ttu-id="28eb5-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="28eb5-247">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="28eb5-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="28eb5-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28eb5-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="28eb5-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28eb5-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="28eb5-250">Testing single sign-on</span></span>

<span data-ttu-id="28eb5-251">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="28eb5-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="28eb5-252">Al hacer clic en el icono de xMatters OnDemand en el panel de acceso, debería iniciar sesión automáticamente en la aplicación xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="28eb5-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="28eb5-253">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28eb5-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28eb5-254">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="28eb5-254">Additional resources</span></span>

* [<span data-ttu-id="28eb5-255">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28eb5-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28eb5-256">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28eb5-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

