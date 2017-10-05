---
title: "Tutorial: Integración de Azure Active Directory con Zendesk | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="593b0-103">Tutorial: Integración de Azure Active Directory con Zendesk</span><span class="sxs-lookup"><span data-stu-id="593b0-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="593b0-104">En este tutorial, aprenderá a integrar Zendesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="593b0-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="593b0-105">La integración de Zendesk con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="593b0-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="593b0-106">Puede controlar en Azure AD quién tiene acceso a Zendesk.</span><span class="sxs-lookup"><span data-stu-id="593b0-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="593b0-107">Puede permitir que los usuarios inicien sesión automáticamente en Zendesk (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="593b0-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="593b0-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="593b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="593b0-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="593b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="593b0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="593b0-110">Prerequisites</span></span>

<span data-ttu-id="593b0-111">Para configurar la integración de Azure AD con Zendesk, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="593b0-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="593b0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="593b0-113">Una suscripción habilitada para el inicio de sesión único en Zendesk</span><span class="sxs-lookup"><span data-stu-id="593b0-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="593b0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="593b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="593b0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="593b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="593b0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="593b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="593b0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="593b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="593b0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="593b0-118">Scenario description</span></span>
<span data-ttu-id="593b0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="593b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="593b0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="593b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="593b0-121">Adición de Zendesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="593b0-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="593b0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="593b0-123">Adición de Zendesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="593b0-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="593b0-124">Para configurar la integración de Zendesk en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="593b0-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="593b0-125">**Para agregar Zendesk desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="593b0-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="593b0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="593b0-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="593b0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="593b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="593b0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="593b0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="593b0-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="593b0-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="593b0-133">En el cuadro de búsqueda, escriba **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="593b0-133">In the search box, type **Zendesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="593b0-135">En el panel de resultados, seleccione  **Zendesk** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="593b0-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="593b0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="593b0-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zendesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="593b0-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="593b0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Zendesk para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="593b0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="593b0-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Zendesk.</span><span class="sxs-lookup"><span data-stu-id="593b0-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="593b0-141">Esta relación de vínculo se establece asignando el valor de **nombre de usuario** de Azure AD como el valor de **nombre de usuario** de Zendesk.</span><span class="sxs-lookup"><span data-stu-id="593b0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="593b0-142">Para configurar y probar el inicio de sesión único de Azure AD con Zendesk, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="593b0-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="593b0-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="593b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="593b0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="593b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="593b0-145">**[Creación de un usuario de prueba de Zendesk](#creating-a-zendesk-test-user)**: el objetivo es tener un homólogo de Britta Simon en  Zendesk que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="593b0-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="593b0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="593b0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="593b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="593b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="593b0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="593b0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Zendesk.</span><span class="sxs-lookup"><span data-stu-id="593b0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="593b0-150">**Para configurar el inicio de sesión único de Azure AD con Zendesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="593b0-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="593b0-151">En la página de integración de la aplicación  **Zendesk** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="593b0-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="593b0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="593b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="593b0-155">En la sección **Dominio y direcciones URL de Zendesk**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="593b0-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="593b0-157">a.</span><span class="sxs-lookup"><span data-stu-id="593b0-157">a.</span></span> <span data-ttu-id="593b0-158">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="593b0-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="593b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="593b0-159">b.</span></span> <span data-ttu-id="593b0-160">En el cuadro de texto **Identificador**, escriba el valor con el siguiente patrón: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="593b0-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="593b0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="593b0-161">These values are not real.</span></span> <span data-ttu-id="593b0-162">Actualícelos con los valores reales de dirección URL de inicio de sesión e identificador.</span><span class="sxs-lookup"><span data-stu-id="593b0-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="593b0-163">Póngase en contacto con el [equipo de soporte técnico de Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="593b0-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="593b0-164">La aplicación Zendesk espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="593b0-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="593b0-165">No hay ningún atributo SAML obligatorio, pero opcionalmente puede agregar un atributo desde la sección **Atributos de usuario** mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="593b0-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="593b0-167">a.</span><span class="sxs-lookup"><span data-stu-id="593b0-167">a.</span></span> <span data-ttu-id="593b0-168">Haga clic en la casilla **View and edit all the other attributes** (Ver y editar todos los demás atributos).</span><span class="sxs-lookup"><span data-stu-id="593b0-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="593b0-170">b.</span><span class="sxs-lookup"><span data-stu-id="593b0-170">b.</span></span> <span data-ttu-id="593b0-171">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="593b0-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="593b0-173">c.</span><span class="sxs-lookup"><span data-stu-id="593b0-173">c.</span></span> <span data-ttu-id="593b0-174">En el cuadro de texto **Nombre**, escriba el nombre del atributo (por ejemplo, **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="593b0-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="593b0-175">d.</span><span class="sxs-lookup"><span data-stu-id="593b0-175">d.</span></span> <span data-ttu-id="593b0-176">En la lista **Valor**, seleccione el valor del atributo (como **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="593b0-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="593b0-177">e.</span><span class="sxs-lookup"><span data-stu-id="593b0-177">e.</span></span> <span data-ttu-id="593b0-178">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="593b0-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="593b0-179">Los atributos de extensión se usan para agregar atributos que, de forma predeterminada, no están en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="593b0-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="593b0-180">Haga clic en [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) (Atributos de usuario que se pueden usar en SAML) para obtener la lista de atributos que acepta **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="593b0-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="593b0-181">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="593b0-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="593b0-183">En la sección **Configuración de Zendesk**, haga clic en **Configurar Zendesk** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="593b0-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="593b0-184">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="593b0-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="593b0-186">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zendesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="593b0-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="593b0-187">Haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="593b0-187">Click **Admin**.</span></span>

9. <span data-ttu-id="593b0-188">En el panel de navegación izquierdo, haga clic en **Settings** (Configuración) y luego en **Security** (Seguridad).</span><span class="sxs-lookup"><span data-stu-id="593b0-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="593b0-189">En la pestaña **Security** (Seguridad), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="593b0-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="593b0-190">![Seguridad](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="593b0-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="593b0-191">![Inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="593b0-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="593b0-192">a.</span><span class="sxs-lookup"><span data-stu-id="593b0-192">a.</span></span> <span data-ttu-id="593b0-193">Haga clic en la pestaña **Admin & Agents** (Administración y agentes).</span><span class="sxs-lookup"><span data-stu-id="593b0-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="593b0-194">b.</span><span class="sxs-lookup"><span data-stu-id="593b0-194">b.</span></span> <span data-ttu-id="593b0-195">Seleccione **Single sign-on (SSO) and SAML** (Inicio de sesión único (SSO) y SAML) y, luego, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="593b0-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="593b0-196">c.</span><span class="sxs-lookup"><span data-stu-id="593b0-196">c.</span></span> <span data-ttu-id="593b0-197">En el cuadro de texto **SAML SSO URL** (Dirección URL de inicio de sesión único de SAML), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="593b0-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="593b0-198">d.</span><span class="sxs-lookup"><span data-stu-id="593b0-198">d.</span></span> <span data-ttu-id="593b0-199">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión remoto), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="593b0-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="593b0-200">e.</span><span class="sxs-lookup"><span data-stu-id="593b0-200">e.</span></span> <span data-ttu-id="593b0-201">En el cuadro de texto **Certificate Fingerprint** (Huella digital de certificado), pegue el valor de **Huella digital** del certificado que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="593b0-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="593b0-202">f.</span><span class="sxs-lookup"><span data-stu-id="593b0-202">f.</span></span> <span data-ttu-id="593b0-203">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="593b0-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="593b0-204">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="593b0-205">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="593b0-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="593b0-207">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="593b0-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="593b0-208">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="593b0-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="593b0-210">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="593b0-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="593b0-212">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="593b0-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="593b0-214">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="593b0-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="593b0-216">a.</span><span class="sxs-lookup"><span data-stu-id="593b0-216">a.</span></span> <span data-ttu-id="593b0-217">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="593b0-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="593b0-218">b.</span><span class="sxs-lookup"><span data-stu-id="593b0-218">b.</span></span> <span data-ttu-id="593b0-219">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="593b0-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="593b0-220">c.</span><span class="sxs-lookup"><span data-stu-id="593b0-220">c.</span></span> <span data-ttu-id="593b0-221">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="593b0-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="593b0-222">d.</span><span class="sxs-lookup"><span data-stu-id="593b0-222">d.</span></span> <span data-ttu-id="593b0-223">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="593b0-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="593b0-224">Creación de un usuario de prueba de Zendesk</span><span class="sxs-lookup"><span data-stu-id="593b0-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="593b0-225">Para que los usuarios de Azure AD puedan iniciar sesión en **Zendesk**, deben aprovisionarse en **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="593b0-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="593b0-226">El comportamiento esperado depende del rol asignado en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="593b0-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="593b0-227">Las cuentas de **usuario final** se aprovisionan automáticamente al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="593b0-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="593b0-228">Las cuentas de **agente** y **administrador** se deben aprovisionar manualmente en **Zendesk** antes de iniciar la sesión.</span><span class="sxs-lookup"><span data-stu-id="593b0-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="593b0-229">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="593b0-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="593b0-230">Inicie sesión en su inquilino de **Zendesk** .</span><span class="sxs-lookup"><span data-stu-id="593b0-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="593b0-231">Seleccione la pestaña **Customer List** (Lista de clientes).</span><span class="sxs-lookup"><span data-stu-id="593b0-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="593b0-232">Seleccione la pestaña **User** (Usuario) y haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="593b0-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="593b0-233">![Agregar usuario](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="593b0-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="593b0-234">Escriba la dirección de correo electrónico de una cuenta de Azure AD existente que quiera aprovisionar y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="593b0-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="593b0-235">![Nuevo usuario](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="593b0-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="593b0-236">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Zendesk ofrecida por Zendesk para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="593b0-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="593b0-237">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="593b0-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="593b0-238">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Zendesk.</span><span class="sxs-lookup"><span data-stu-id="593b0-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="593b0-240">**Para asignar Britta Simon a Zendesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="593b0-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="593b0-241">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="593b0-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="593b0-243">En la lista de aplicaciones, seleccione **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="593b0-243">In the applications list, select **Zendesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="593b0-245">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="593b0-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="593b0-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="593b0-247">Click **Add** button.</span></span> <span data-ttu-id="593b0-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="593b0-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="593b0-250">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="593b0-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="593b0-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="593b0-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="593b0-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="593b0-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="593b0-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="593b0-253">Testing single sign-on</span></span>

<span data-ttu-id="593b0-254">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="593b0-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="593b0-255">Al hacer clic en el icono de Zendesk en el Panel de acceso, debería iniciar sesión automáticamente en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="593b0-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="593b0-256">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="593b0-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="593b0-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="593b0-257">Additional resources</span></span>

* [<span data-ttu-id="593b0-258">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="593b0-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="593b0-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="593b0-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
