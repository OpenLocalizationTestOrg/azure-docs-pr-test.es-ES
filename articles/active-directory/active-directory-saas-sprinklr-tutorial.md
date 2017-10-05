---
title: "Tutorial: Integración de Azure Active Directory con Sprinklr | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="a5c6d-103">Tutorial: integración de Azure Active Directory con Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5c6d-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="a5c6d-104">En este tutorial, obtendrá información sobre cómo integrar Sprinklr con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5c6d-105">La integración de Sprinklr con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5c6d-106">Puede controlar en Azure AD quién tiene acceso a Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="a5c6d-107">Puede habilitar que los usuarios inicien sesión automáticamente en Sprinklr (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5c6d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5c6d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5c6d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5c6d-110">Prerequisites</span></span>

<span data-ttu-id="a5c6d-111">Para configurar la integración de Azure AD con Sprinklr, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="a5c6d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5c6d-113">Una suscripción habilitada para el inicio de sesión único en Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5c6d-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5c6d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5c6d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5c6d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5c6d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5c6d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a5c6d-118">Scenario description</span></span>
<span data-ttu-id="a5c6d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5c6d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5c6d-121">Incorporación de Sprinklr desde la galería</span><span class="sxs-lookup"><span data-stu-id="a5c6d-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="a5c6d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="a5c6d-123">Incorporación de Sprinklr desde la galería</span><span class="sxs-lookup"><span data-stu-id="a5c6d-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="a5c6d-124">Para configurar la integración de Sprinklr en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5c6d-125">**Para agregar Sprinklr desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a5c6d-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c6d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5c6d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5c6d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a5c6d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a5c6d-133">En el cuadro de búsqueda, escriba **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-133">In the search box, type **Sprinklr**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="a5c6d-135">En el panel de resultados, seleccione **Sprinklr** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5c6d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5c6d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sprinklr con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5c6d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Sprinklr para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="a5c6d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="a5c6d-141">Para establecer la relación de vínculo, en Sprinklr, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5c6d-142">Para configurar y probar el inicio de sesión único de Azure AD con Sprinklr, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5c6d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5c6d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5c6d-145">**[Creación de un usuario de prueba de Sprinklr](#creating-a-sprinklr-test-user)**: para tener un homólogo de Britta Simon en Sprinklr vinculado a la representación del usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5c6d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5c6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5c6d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5c6d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="a5c6d-150">**Para configurar el inicio de sesión único de Azure AD con Sprinklr, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a5c6d-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c6d-151">En Azure Portal, en la página de integración de la aplicación **Sprinklr**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a5c6d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="a5c6d-155">En la sección **Sprinklr Domain and URLs** (Dominio y direcciones URL de Sprinklr), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="a5c6d-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-157">a.</span></span> <span data-ttu-id="a5c6d-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.sprinklr.com`.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="a5c6d-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-159">b.</span></span> <span data-ttu-id="a5c6d-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a5c6d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5c6d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-161">These values are not real.</span></span> <span data-ttu-id="a5c6d-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5c6d-163">Póngase en contacto con el [equipo de soporte técnico de Sprinklr](https://www.sprinklr.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="a5c6d-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="a5c6d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a5c6d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5c6d-168">En la sección **Sprinklr Configuration** (Configuración de Sprinklr), haga clic en **Configure Sprinklr** (Configurar Sprinklr) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5c6d-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="a5c6d-170">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Sprinklr como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="a5c6d-171">Vaya a **Administración \> Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a5c6d-172">![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="a5c6d-173">Vaya a **Administrar socios \> Inicio de sesión único** en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="a5c6d-174">![Administración de asociado](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Administración de asociados")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="a5c6d-175">Haga clic en **+Add Single Sign On**(+ Agregar inicios de sesión únicos).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="a5c6d-176">![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Inicios de sesión únicos")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="a5c6d-177">Siga estos pasos en la página **Inicio de sesión único** :</span><span class="sxs-lookup"><span data-stu-id="a5c6d-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="a5c6d-178">![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Inicios de sesión únicos")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="a5c6d-179">a.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-179">a.</span></span> <span data-ttu-id="a5c6d-180">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración (por ejemplo, *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="a5c6d-181">b.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-181">b.</span></span> <span data-ttu-id="a5c6d-182">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-182">Select **Enabled**.</span></span>

    <span data-ttu-id="a5c6d-183">c.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-183">c.</span></span> <span data-ttu-id="a5c6d-184">Seleccione **Use new SSO Certificate**(Usar el nuevo certificado de SSO).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="a5c6d-185">e.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-185">e.</span></span> <span data-ttu-id="a5c6d-186">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="a5c6d-187">f.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-187">f.</span></span> <span data-ttu-id="a5c6d-188">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **Entity ID** (Id. de entidad).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="a5c6d-189">g.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-189">g.</span></span> <span data-ttu-id="a5c6d-190">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **Identity provider Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a5c6d-191">h.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-191">h.</span></span> <span data-ttu-id="a5c6d-192">Pegue el valor de **Sign-Out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **Identity Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="a5c6d-193">i.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-193">i.</span></span> <span data-ttu-id="a5c6d-194">Como **Tipo de Id. de usuario de SAML**, seleccione **La aserción contiene el nombre de usuario de sprinklr.com del usuario**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="a5c6d-195">j.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-195">j.</span></span> <span data-ttu-id="a5c6d-196">Para **Ubicación de Id. de usuario de SAML**, seleccione **El Id. de usuario está en el elemento NameIdentifier de la instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="a5c6d-197">k.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-197">k.</span></span> <span data-ttu-id="a5c6d-198">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-198">Click **Save**.</span></span>
       
    <span data-ttu-id="a5c6d-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="a5c6d-200">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5c6d-201">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5c6d-202">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5c6d-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5c6d-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5c6d-204">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a5c6d-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a5c6d-206">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a5c6d-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c6d-207">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5c6d-209">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5c6d-211">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5c6d-213">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5c6d-215">a.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-215">a.</span></span> <span data-ttu-id="a5c6d-216">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5c6d-217">b.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-217">b.</span></span> <span data-ttu-id="a5c6d-218">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5c6d-219">c.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-219">c.</span></span> <span data-ttu-id="a5c6d-220">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5c6d-221">d.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-221">d.</span></span> <span data-ttu-id="a5c6d-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="a5c6d-223">Creación de un usuario de prueba de Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5c6d-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="a5c6d-224">Inicie sesión en su sitio de la compañía de Sprinklr como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="a5c6d-225">Vaya a **Administración \> Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a5c6d-226">![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="a5c6d-227">Vaya a **Administrar clientes \> Usuarios** en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="a5c6d-228">![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="a5c6d-229">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="a5c6d-230">![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="a5c6d-231">En el cuadro de diálogo **Edit user** (Editar usuario), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a5c6d-232">![Edición de usuarios](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edición de usuarios")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="a5c6d-233">a.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-233">a.</span></span> <span data-ttu-id="a5c6d-234">En los cuadros de texto **Correo electrónico**, **Nombre** y **Apellido**, escriba la información de una cuenta de usuario de Azure AD que desee aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="a5c6d-235">b.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-235">b.</span></span> <span data-ttu-id="a5c6d-236">Seleccione **Password Disabled**(Contraseña deshabilitada).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="a5c6d-237">c.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-237">c.</span></span> <span data-ttu-id="a5c6d-238">Seleccione **Language** (Lenguaje).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-238">Select **Language**.</span></span>

    <span data-ttu-id="a5c6d-239">d.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-239">d.</span></span> <span data-ttu-id="a5c6d-240">Seleccione **User Type**(Tipo de usuario).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-240">Select **User Type**.</span></span>

    <span data-ttu-id="a5c6d-241">e.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-241">e.</span></span> <span data-ttu-id="a5c6d-242">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="a5c6d-243">**Password Disabled** (Contraseña deshabilitada) debe estar seleccionada para que los usuarios puedan iniciar sesión a través de un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="a5c6d-244">Vaya a **Role**(Rol) y luego lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a5c6d-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="a5c6d-245">![Roles de asociados](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Roles de asociados")</span><span class="sxs-lookup"><span data-stu-id="a5c6d-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="a5c6d-246">a.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-246">a.</span></span> <span data-ttu-id="a5c6d-247">En la lista **Global**, seleccione **ALL\_Permissions** (TODOS los permisos).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="a5c6d-248">b.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-248">b.</span></span> <span data-ttu-id="a5c6d-249">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="a5c6d-250">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Sprinklr ofrecida por Sprinklr para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5c6d-251">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5c6d-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5c6d-252">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a5c6d-254">**Para asignar a Britta Simon a Sprinklr, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a5c6d-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c6d-255">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a5c6d-257">En la lista de aplicaciones, seleccione **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-257">In the applications list, select **Sprinklr**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="a5c6d-259">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a5c6d-261">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-261">Click **Add** button.</span></span> <span data-ttu-id="a5c6d-262">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a5c6d-264">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5c6d-265">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5c6d-266">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5c6d-267">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a5c6d-267">Testing single sign-on</span></span>

<span data-ttu-id="a5c6d-268">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a5c6d-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5c6d-269">Al hacer clic en el icono de Sprinklr del Panel de acceso, se inicia sesión en la aplicación Sprinklr automáticamente. Para más información sobre el Panel de acceso, consulte la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5c6d-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a5c6d-270">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a5c6d-270">Additional resources</span></span>

* [<span data-ttu-id="a5c6d-271">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5c6d-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5c6d-272">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5c6d-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

