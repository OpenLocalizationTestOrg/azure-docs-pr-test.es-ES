---
title: "Tutorial: Integración de Azure Active Directory con NetSuite | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y NetSuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="fdcfa-103">Tutorial: Integración de Azure Active Directory con NetSuite</span><span class="sxs-lookup"><span data-stu-id="fdcfa-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="fdcfa-104">En este tutorial, obtendrá información sobre cómo integrar NetSuite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdcfa-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdcfa-105">La integración de NetSuite con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fdcfa-106">En Azure AD puede controlar quién tiene acceso a NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="fdcfa-107">Puede permitir que los usuarios inicien sesión automáticamente en NetSuite (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fdcfa-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fdcfa-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fdcfa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdcfa-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fdcfa-110">Prerequisites</span></span>

<span data-ttu-id="fdcfa-111">Para configurar la integración de Azure AD con NetSuite, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="fdcfa-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdcfa-113">Una suscripción habilitada para el inicio de sesión único en NetSuite</span><span class="sxs-lookup"><span data-stu-id="fdcfa-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdcfa-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdcfa-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdcfa-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fdcfa-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdcfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdcfa-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fdcfa-118">Scenario description</span></span>
<span data-ttu-id="fdcfa-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdcfa-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdcfa-121">Incorporación de NetSuite desde la galería</span><span class="sxs-lookup"><span data-stu-id="fdcfa-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="fdcfa-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="fdcfa-123">Incorporación de NetSuite desde la galería</span><span class="sxs-lookup"><span data-stu-id="fdcfa-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="fdcfa-124">Para configurar la integración de NetSuite en Azure AD, deberá agregar NetSuite desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fdcfa-125">**Para agregar NetSuite desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fdcfa-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fdcfa-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fdcfa-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fdcfa-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fdcfa-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fdcfa-133">En el cuadro de búsqueda, escriba **NetSuite**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-133">In the search box, type **Netsuite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="fdcfa-135">En el panel de resultados, seleccione **NetSuite** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fdcfa-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fdcfa-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con NetSuite con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fdcfa-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fdcfa-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de NetSuite para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="fdcfa-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="fdcfa-141">Para establecer esta relación de vínculo, en NetSuite, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="fdcfa-142">Para configurar y probar el inicio de sesión único de Azure AD con NetSuite, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fdcfa-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fdcfa-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdcfa-145">**[Creación de un usuario de prueba de NetSuite](#creating-a-netsuite-test-user)**: para tener un homólogo de Britta Simon en NetSuite vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fdcfa-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdcfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fdcfa-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fdcfa-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="fdcfa-150">**Para configurar el inicio de sesión único de Azure AD con NetSuite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fdcfa-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="fdcfa-151">En Azure Portal, en la página de integración de la aplicación **NetSuite**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fdcfa-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="fdcfa-155">En la sección **Dominio y direcciones URL de NetSuite**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="fdcfa-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="fdcfa-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fdcfa-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-158">This value is not real value.</span></span> <span data-ttu-id="fdcfa-159">Actualícelo con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="fdcfa-160">Póngase en contacto con el [equipo de soporte técnico de NetSuite](http://www.netsuite.com/portal/services/support.shtml) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="fdcfa-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="fdcfa-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fdcfa-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fdcfa-165">En la sección **Configuración de NetSuite**, haga clic en **Configurar NetSuite** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fdcfa-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="fdcfa-168">Abra una nueva pestaña en el explorador e inicie sesión en el sitio de la empresa Netsuite como administrador.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="fdcfa-169">En la barra de herramientas en la parte superior de la página, haga clic en **Configuración** y haga clic en **Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="fdcfa-171">En la lista **Tareas de configuración**, seleccione **Integración**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="fdcfa-173">En la sección **Administrar autenticación**, haga clic en **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="fdcfa-175">En la página **Configuración de SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="fdcfa-176">a.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-176">a.</span></span> <span data-ttu-id="fdcfa-177">Copie el valor de la **dirección URL del servicio de inicio de sesión único de SAML** de la sección de **referencia rápida** de **Configuración de inicio de sesión** y péguelo en el campo **Identity Provider Login Page** (Página de inicio de sesión del proveedor de identidades) en NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="fdcfa-179">b.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-179">b.</span></span> <span data-ttu-id="fdcfa-180">En NetSuite, seleccione **Primary Authentication Method** (Método de autenticación principal).</span><span class="sxs-lookup"><span data-stu-id="fdcfa-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="fdcfa-181">c.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-181">c.</span></span> <span data-ttu-id="fdcfa-182">Para el campo con la etiqueta **Metadatos del proveedor de identidades de SAMLV2**, seleccione **Cargar archivo de metadatos de IDP**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="fdcfa-183">A continuación, haga clic en **Examinar** para cargar el archivo de metadatos que descargó de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="fdcfa-185">d.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-185">d.</span></span> <span data-ttu-id="fdcfa-186">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-186">Click **Submit**.</span></span>

12. <span data-ttu-id="fdcfa-187">En Azure AD, haga clic en la casilla **Ver y editar todos los atributos de usuario** y agregue el atributo.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="fdcfa-189">Para el campo **Nombre de atributo**, escriba `account`.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="fdcfa-190">En el campo **Attribute Value** (Valor de atributo), escriba el identificador de la cuenta de NetSuite. Este valor es constante y cambia con la cuenta.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="fdcfa-191">A continuación se incluyen instrucciones sobre cómo encontrar el identificador de la cuenta:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-191">Instructions on how to find your account ID are included below:</span></span>

      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="fdcfa-193">a.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-193">a.</span></span> <span data-ttu-id="fdcfa-194">En NetSuite, haga clic en **Setup** (Configurar) en el menú de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="fdcfa-195">b.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-195">b.</span></span> <span data-ttu-id="fdcfa-196">A continuación, haga clic en la sección **Tareas de configuración** del menú de navegación izquierdo, seleccione la sección **Integración** y haga clic en **Preferencias de servicios web**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="fdcfa-197">c.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-197">c.</span></span> <span data-ttu-id="fdcfa-198">Copie el identificador de la cuenta NetSuite y péguelo en el campo **Valor del atributo** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="fdcfa-200">Antes de que los usuarios puedan realizar el inicio de sesión único en NetSuite, se les deben asignar primero los permisos adecuados en NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="fdcfa-201">Siga las instrucciones siguientes para asignar estos permisos.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="fdcfa-202">a.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-202">a.</span></span> <span data-ttu-id="fdcfa-203">En el menú de navegación superior, haga clic en **Configuración** y en **Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="fdcfa-205">b.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-205">b.</span></span> <span data-ttu-id="fdcfa-206">En el menú de navegación izquierdo, seleccione **Usuarios/Roles** y haga clic en **Administrar roles**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="fdcfa-208">c.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-208">c.</span></span> <span data-ttu-id="fdcfa-209">Haga clic en **Nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-209">Click **New Role**.</span></span>

    <span data-ttu-id="fdcfa-210">d.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-210">d.</span></span> <span data-ttu-id="fdcfa-211">Escriba un **Nombre** para el nuevo rol y active la casilla **Solo inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="fdcfa-213">e.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-213">e.</span></span> <span data-ttu-id="fdcfa-214">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-214">Click **Save**.</span></span>

    <span data-ttu-id="fdcfa-215">f.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-215">f.</span></span> <span data-ttu-id="fdcfa-216">En el menú de la parte superior, haga clic en **Permisos**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="fdcfa-217">A continuación, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-217">Then click **Setup**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="fdcfa-219">g.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-219">g.</span></span> <span data-ttu-id="fdcfa-220">Seleccione **Configurar inicio de sesión único de SAM** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="fdcfa-221">h.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-221">h.</span></span> <span data-ttu-id="fdcfa-222">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-222">Click **Save**.</span></span>

    <span data-ttu-id="fdcfa-223">i.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-223">i.</span></span> <span data-ttu-id="fdcfa-224">En el menú de navegación superior, haga clic en **Configuración** y en **Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="fdcfa-226">j.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-226">j.</span></span> <span data-ttu-id="fdcfa-227">En el menú de navegación izquierdo, seleccione **Usuarios/Roles** y haga clic en **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="fdcfa-229">k.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-229">k.</span></span> <span data-ttu-id="fdcfa-230">Seleccione un usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-230">Select a test user.</span></span> <span data-ttu-id="fdcfa-231">A continuación, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-231">Then click **Edit**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="fdcfa-233">l.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-233">l.</span></span> <span data-ttu-id="fdcfa-234">En el cuadro de diálogo Roles, seleccione el rol que se ha creado y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="fdcfa-236">m.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-236">m.</span></span> <span data-ttu-id="fdcfa-237">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="fdcfa-238">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fdcfa-239">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fdcfa-240">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fdcfa-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fdcfa-241">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="fdcfa-242">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fdcfa-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fdcfa-244">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="fdcfa-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fdcfa-245">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="fdcfa-247">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fdcfa-249">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fdcfa-251">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fdcfa-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fdcfa-253">a.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-253">a.</span></span> <span data-ttu-id="fdcfa-254">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdcfa-255">b.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-255">b.</span></span> <span data-ttu-id="fdcfa-256">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fdcfa-257">c.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-257">c.</span></span> <span data-ttu-id="fdcfa-258">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fdcfa-259">d.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-259">d.</span></span> <span data-ttu-id="fdcfa-260">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="fdcfa-261">Creación de un usuario de prueba de NetSuite</span><span class="sxs-lookup"><span data-stu-id="fdcfa-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="fdcfa-262">En esta sección se creará un usuario llamado Britta Simon en NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="fdcfa-263">NetSuite admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="fdcfa-264">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-264">There is no action item for you in this section.</span></span> <span data-ttu-id="fdcfa-265">Si el usuario ya no existe en NetSuite, se crea uno nuevo cuando se intenta acceder a NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fdcfa-266">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdcfa-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fdcfa-267">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a NetSuite.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fdcfa-269">**Para asignar a Britta Simon a NetSuite, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="fdcfa-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="fdcfa-270">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fdcfa-272">En la lista de aplicaciones, seleccione **NetSuite**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-272">In the applications list, select **Netsuite**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="fdcfa-274">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fdcfa-276">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-276">Click **Add** button.</span></span> <span data-ttu-id="fdcfa-277">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fdcfa-279">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fdcfa-280">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdcfa-281">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fdcfa-282">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fdcfa-282">Testing single sign-on</span></span>

<span data-ttu-id="fdcfa-283">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fdcfa-284">Para probar la configuración de inicios de sesión únicos, abra el Panel de acceso en [https://myapps.microsoft.com](https://myapps.microsoft.com/), inicie sesión en la cuenta de prueba y haga clic en **NetSuite**.</span><span class="sxs-lookup"><span data-stu-id="fdcfa-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdcfa-285">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fdcfa-285">Additional resources</span></span>

* [<span data-ttu-id="fdcfa-286">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdcfa-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdcfa-287">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fdcfa-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fdcfa-288">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="fdcfa-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

