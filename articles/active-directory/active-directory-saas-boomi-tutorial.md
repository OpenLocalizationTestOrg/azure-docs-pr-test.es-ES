---
title: "Tutorial: Integración de Azure Active Directory con Boomi | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="a1430-103">Tutorial: Integración de Azure Active Directory con Boomi</span><span class="sxs-lookup"><span data-stu-id="a1430-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="a1430-104">En este tutorial, aprenderá a integrar Boomi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1430-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1430-105">La integración de Boomi con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a1430-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1430-106">Puede controlar en Azure AD quién tiene acceso a Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="a1430-107">Puede permitir que los usuarios inicien sesión automáticamente en Boomi (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1430-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1430-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1430-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a1430-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1430-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1430-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a1430-110">Prerequisites</span></span>

<span data-ttu-id="a1430-111">Para configurar la integración de Azure AD con Boomi, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a1430-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="a1430-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1430-113">Una suscripción habilitada para inicio de sesión único en Boomi</span><span class="sxs-lookup"><span data-stu-id="a1430-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1430-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a1430-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1430-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a1430-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1430-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a1430-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1430-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1430-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1430-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a1430-118">Scenario description</span></span>
<span data-ttu-id="a1430-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a1430-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1430-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a1430-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1430-121">Adición de Boomi desde la galería</span><span class="sxs-lookup"><span data-stu-id="a1430-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="a1430-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="a1430-123">Adición de Boomi desde la galería</span><span class="sxs-lookup"><span data-stu-id="a1430-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="a1430-124">Para configurar la integración de Boomi en Azure AD, deberá agregar Boomi desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a1430-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1430-125">**Para agregar Boomi desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a1430-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1430-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1430-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1430-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a1430-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1430-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a1430-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a1430-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1430-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a1430-133">En el cuadro de búsqueda, escriba **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="a1430-133">In the search box, type **Boomi**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="a1430-135">En el panel de resultados, seleccione **Boomi** y luego haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1430-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1430-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1430-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Boomi con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1430-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1430-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Boomi para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1430-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="a1430-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="a1430-141">Para establecer la relación de vínculo, en Boomi, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a1430-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a1430-142">Para configurar y probar el inicio de sesión único de Azure AD con Boomi, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a1430-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1430-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a1430-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1430-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1430-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1430-145">**[Creación de un usuario de prueba de Boomi](#creating-a-boomi-test-user)**: para tener un homólogo de Britta Simon en Boomi que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1430-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1430-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1430-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1430-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a1430-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1430-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1430-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="a1430-150">**Para configurar el inicio de sesión único de Azure AD con Boomi, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a1430-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="a1430-151">En Azure Portal, en la página de integración de la aplicación **Boomi**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a1430-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a1430-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a1430-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="a1430-155">En la sección **Dominio y direcciones URL de Boomi**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1430-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="a1430-157">a.</span><span class="sxs-lookup"><span data-stu-id="a1430-157">a.</span></span> <span data-ttu-id="a1430-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="a1430-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="a1430-159">b.</span><span class="sxs-lookup"><span data-stu-id="a1430-159">b.</span></span> <span data-ttu-id="a1430-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://platform.boomi.com/sso/<accountname>/saml`.</span><span class="sxs-lookup"><span data-stu-id="a1430-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1430-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a1430-161">These values are not real.</span></span> <span data-ttu-id="a1430-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="a1430-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a1430-163">Póngase en contacto con el [equipo de soporte técnico de Boomi](https://boomi.com/company/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="a1430-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="a1430-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a1430-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="a1430-166">La aplicación Boomi espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="a1430-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a1430-167">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1430-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="a1430-168">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a1430-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a1430-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="a1430-169">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="a1430-171">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, para cada fila que se muestra en la tabla siguiente, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1430-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="a1430-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="a1430-172">Attribute Name</span></span> | <span data-ttu-id="a1430-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="a1430-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="a1430-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="a1430-174">FEDERATION_ID</span></span> | <span data-ttu-id="a1430-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="a1430-175">user.mail</span></span> |
    
    <span data-ttu-id="a1430-176">a.</span><span class="sxs-lookup"><span data-stu-id="a1430-176">a.</span></span> <span data-ttu-id="a1430-177">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="a1430-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a1430-180">b.</span><span class="sxs-lookup"><span data-stu-id="a1430-180">b.</span></span> <span data-ttu-id="a1430-181">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="a1430-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a1430-182">c.</span><span class="sxs-lookup"><span data-stu-id="a1430-182">c.</span></span> <span data-ttu-id="a1430-183">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="a1430-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a1430-184">d.</span><span class="sxs-lookup"><span data-stu-id="a1430-184">d.</span></span> <span data-ttu-id="a1430-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a1430-185">Click **Ok**.</span></span>

6. <span data-ttu-id="a1430-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a1430-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a1430-188">En la sección **Configuración de Boomi**, haga clic en **Configurar Boomi** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a1430-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a1430-189">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a1430-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="a1430-191">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="a1430-192">Vaya a **Company Name** (Nombre de la compañía) y haga clic en **Set up** (Configurar).</span><span class="sxs-lookup"><span data-stu-id="a1430-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="a1430-193">Haga clic en la pestaña **SSO Options** (Opciones de SSO) y realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="a1430-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="a1430-195">a.</span><span class="sxs-lookup"><span data-stu-id="a1430-195">a.</span></span> <span data-ttu-id="a1430-196">Marque la casilla **Enable SAML Single Sign-On** (Habilitar el inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="a1430-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="a1430-197">b.</span><span class="sxs-lookup"><span data-stu-id="a1430-197">b.</span></span> <span data-ttu-id="a1430-198">Haga clic en **Import** (Importar) para cargar el certificado descargado de Azure AD en **Identity Provider Certificate** (Certificado del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="a1430-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="a1430-199">c.</span><span class="sxs-lookup"><span data-stu-id="a1430-199">c.</span></span> <span data-ttu-id="a1430-200">En el cuadro de texto **URL de inicio de sesión del proveedor de identidades**, coloque el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) en la ventana de configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1430-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="a1430-201">d.</span><span class="sxs-lookup"><span data-stu-id="a1430-201">d.</span></span> <span data-ttu-id="a1430-202">Como **ubicación del identificador de federación**, seleccione el botón de radio **Federation Id is in FEDERATION_ID Attribute element** (El id. de federación está en el elemento de atributo FEDERATION_ID).</span><span class="sxs-lookup"><span data-stu-id="a1430-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="a1430-203">e.</span><span class="sxs-lookup"><span data-stu-id="a1430-203">e.</span></span> <span data-ttu-id="a1430-204">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a1430-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a1430-205">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1430-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1430-206">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a1430-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1430-207">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1430-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1430-208">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1430-209">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1430-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a1430-211">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a1430-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1430-212">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1430-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1430-214">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a1430-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1430-216">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1430-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1430-218">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a1430-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1430-220">a.</span><span class="sxs-lookup"><span data-stu-id="a1430-220">a.</span></span> <span data-ttu-id="a1430-221">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1430-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1430-222">b.</span><span class="sxs-lookup"><span data-stu-id="a1430-222">b.</span></span> <span data-ttu-id="a1430-223">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1430-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1430-224">c.</span><span class="sxs-lookup"><span data-stu-id="a1430-224">c.</span></span> <span data-ttu-id="a1430-225">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a1430-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a1430-226">d.</span><span class="sxs-lookup"><span data-stu-id="a1430-226">d.</span></span> <span data-ttu-id="a1430-227">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a1430-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="a1430-228">Creación de un usuario de prueba de Boomi</span><span class="sxs-lookup"><span data-stu-id="a1430-228">Creating a Boomi test user</span></span>

<span data-ttu-id="a1430-229">Para permitir que los usuarios de Azure AD inicien sesión en Boomi, tienen que aprovisionarse en Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="a1430-230">En el caso de Boomi, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="a1430-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="a1430-231">Para aprovisionar una cuenta de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1430-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="a1430-232">Inicie sesión en su sitio de la compañía de Boomi como administrador.</span><span class="sxs-lookup"><span data-stu-id="a1430-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="a1430-233">Después de iniciar sesión, vaya a **User Management** (Administración de usuarios) y vaya a **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="a1430-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="a1430-234">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="a1430-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="a1430-235">Haga clic en el icono **+**, se abre el cuadro de diálogo **Add/Maintain User Roles** (Agregar o mantener roles de usuario).</span><span class="sxs-lookup"><span data-stu-id="a1430-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="a1430-236">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="a1430-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="a1430-237">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="a1430-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="a1430-238">a.</span><span class="sxs-lookup"><span data-stu-id="a1430-238">a.</span></span> <span data-ttu-id="a1430-239">En el cuadro de texto **Dirección de correo electrónico del usuario**, escriba la dirección de correo electrónico de un usuario, por ejemplo, BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a1430-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="a1430-240">b.</span><span class="sxs-lookup"><span data-stu-id="a1430-240">b.</span></span> <span data-ttu-id="a1430-241">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, Britta.</span><span class="sxs-lookup"><span data-stu-id="a1430-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="a1430-242">c.</span><span class="sxs-lookup"><span data-stu-id="a1430-242">c.</span></span> <span data-ttu-id="a1430-243">En el cuadro de texto **Apellidos**, escriba el nombre del usuario, en este caso, Simon.</span><span class="sxs-lookup"><span data-stu-id="a1430-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="a1430-244">d.</span><span class="sxs-lookup"><span data-stu-id="a1430-244">d.</span></span> <span data-ttu-id="a1430-245">Escriba el **id. de federación** del usuario.</span><span class="sxs-lookup"><span data-stu-id="a1430-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="a1430-246">Cada usuario debe tener un id. de federación que identifica de forma única al usuario dentro de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a1430-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="a1430-247">e.</span><span class="sxs-lookup"><span data-stu-id="a1430-247">e.</span></span> <span data-ttu-id="a1430-248">Asigne el rol **Usuario estándar** al usuario.</span><span class="sxs-lookup"><span data-stu-id="a1430-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="a1430-249">No asigne el rol Administrador porque le proporcionaría acceso normal a Atmosphere, así como acceso de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a1430-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="a1430-250">f.</span><span class="sxs-lookup"><span data-stu-id="a1430-250">f.</span></span> <span data-ttu-id="a1430-251">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a1430-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a1430-252">El usuario no recibirá un correo electrónico de notificación de bienvenida con una contraseña que se pueda usar para iniciar sesión en la cuenta de AtomSphere porque su contraseña se administra mediante el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="a1430-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="a1430-253">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Boomi que proporcione Boomi para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="a1430-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a1430-254">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1430-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a1430-255">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a1430-257">**Para asignar Britta Simon a Boomi, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a1430-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="a1430-258">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a1430-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a1430-260">En la lista de aplicaciones, seleccione **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="a1430-260">In the applications list, select **Boomi**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="a1430-262">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a1430-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a1430-264">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a1430-264">Click **Add** button.</span></span> <span data-ttu-id="a1430-265">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a1430-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a1430-267">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a1430-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1430-268">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a1430-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1430-269">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a1430-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1430-270">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a1430-270">Testing single sign-on</span></span>

<span data-ttu-id="a1430-271">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a1430-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a1430-272">Al hacer clic en el icono de Boomi en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Boomi.</span><span class="sxs-lookup"><span data-stu-id="a1430-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1430-273">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a1430-273">Additional resources</span></span>

* [<span data-ttu-id="a1430-274">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1430-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1430-275">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1430-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

