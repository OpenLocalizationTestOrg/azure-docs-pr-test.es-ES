---
title: "Tutorial: Integración de Azure Active Directory con SAP Business ByDesign | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="96f20-103">Tutorial: Integración de Azure Active Directory con SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="96f20-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="96f20-104">En este tutorial, aprenderá a integrar SAP Business ByDesign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96f20-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96f20-105">La integración de SAP Business ByDesign con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="96f20-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96f20-106">Puede controlar en Azure AD quién tiene acceso a SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="96f20-107">Puede permitir que los usuarios inicien sesión automáticamente en SAP Business ByDesign (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f20-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="96f20-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="96f20-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="96f20-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96f20-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f20-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96f20-110">Prerequisites</span></span>

<span data-ttu-id="96f20-111">Para configurar la integración de Azure AD con SAP Business ByDesign, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="96f20-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="96f20-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96f20-113">Una suscripción habilitada para el inicio de sesión único en SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="96f20-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96f20-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="96f20-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96f20-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="96f20-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96f20-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="96f20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96f20-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96f20-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96f20-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="96f20-118">Scenario description</span></span>
<span data-ttu-id="96f20-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="96f20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96f20-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="96f20-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96f20-121">Adición de SAP Business ByDesign desde la galería</span><span class="sxs-lookup"><span data-stu-id="96f20-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="96f20-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="96f20-123">Adición de SAP Business ByDesign desde la galería</span><span class="sxs-lookup"><span data-stu-id="96f20-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="96f20-124">Para configurar la integración de SAP Business ByDesign en Azure AD, es preciso agregar SAP Business ByDesign desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="96f20-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96f20-125">**Para agregar SAP Business ByDesign desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="96f20-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96f20-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96f20-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="96f20-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="96f20-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96f20-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="96f20-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="96f20-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96f20-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="96f20-133">En el cuadro de búsqueda, escriba **SAP Business ByDesign**, seleccione **SAP Business ByDesign** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96f20-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign en la lista de resultados](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="96f20-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="96f20-136">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAP Business ByDesign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96f20-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96f20-137">Para que el inicio de sesión único funcione, es preciso que Azure AD sepa cuál es el usuario homólogo de SAP Business ByDesign para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f20-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="96f20-138">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="96f20-139">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario** en SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="96f20-140">Para configurar y probar el inicio de sesión único de Azure AD con SAP Business ByDesign, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="96f20-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96f20-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="96f20-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96f20-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96f20-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96f20-143">**[Creación de un usuario de prueba de SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**: para tener un homólogo de Britta Simon en SAP Business ByDesign que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f20-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96f20-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f20-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96f20-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="96f20-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="96f20-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="96f20-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="96f20-148">**Para configurar el inicio de sesión único de Azure AD con SAP Business ByDesign, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="96f20-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="96f20-149">En la página de integración de la aplicación **SAP Business ByDesign** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="96f20-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="96f20-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="96f20-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="96f20-153">En la sección **Dominio y direcciones URL de SAP Business ByDesign**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="96f20-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="96f20-155">a.</span><span class="sxs-lookup"><span data-stu-id="96f20-155">a.</span></span> <span data-ttu-id="96f20-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<servername>.sapbydesign.com`.</span><span class="sxs-lookup"><span data-stu-id="96f20-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="96f20-157">b.</span><span class="sxs-lookup"><span data-stu-id="96f20-157">b.</span></span> <span data-ttu-id="96f20-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="96f20-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96f20-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="96f20-159">These values are not real.</span></span> <span data-ttu-id="96f20-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="96f20-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="96f20-161">Póngase en contacto con el [equipo de soporte técnico de SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="96f20-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="96f20-162">En la sección **Atributos de usuario**, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="96f20-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![Sección Atributos de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="96f20-164">a.</span><span class="sxs-lookup"><span data-stu-id="96f20-164">a.</span></span> <span data-ttu-id="96f20-165">En la lista **Identificador de usuario**, seleccione la función **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="96f20-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="96f20-166">b.</span><span class="sxs-lookup"><span data-stu-id="96f20-166">b.</span></span> <span data-ttu-id="96f20-167">En la lista **Correo** , seleccione el atributo de usuario que desea usar en su implementación.</span><span class="sxs-lookup"><span data-stu-id="96f20-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="96f20-168">Por ejemplo, si quiere usar EmployeeID como identificador de usuario único y ha almacenado el valor del atributo en ExtensionAttribute2, seleccione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="96f20-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="96f20-169">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="96f20-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="96f20-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="96f20-171">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="96f20-173">En la sección **Configuración de SAP Business ByDesign**, haga clic en **Configurar SAP Business ByDesign** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="96f20-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="96f20-174">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="96f20-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="96f20-176">Para que SSO se configure para su aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="96f20-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="96f20-177">a.</span><span class="sxs-lookup"><span data-stu-id="96f20-177">a.</span></span> <span data-ttu-id="96f20-178">Inicie sesión en el portal de SAP Business ByDesign con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="96f20-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="96f20-179">b.</span><span class="sxs-lookup"><span data-stu-id="96f20-179">b.</span></span> <span data-ttu-id="96f20-180">Navegue hasta **Application and User Management Common Task** (Tarea común de administración de usuarios y aplicaciones) y haga clic en la pestaña **Proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="96f20-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="96f20-181">c.</span><span class="sxs-lookup"><span data-stu-id="96f20-181">c.</span></span> <span data-ttu-id="96f20-182">Haga clic en **New Identity Provider** (Nuevo proveedor de identidades) y seleccione el archivo XML de metadatos que ha descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="96f20-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="96f20-183">Al importar los metadatos, el sistema carga automáticamente el certificado de firma y el certificado de cifrado necesarios.</span><span class="sxs-lookup"><span data-stu-id="96f20-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="96f20-185">d.</span><span class="sxs-lookup"><span data-stu-id="96f20-185">d.</span></span> <span data-ttu-id="96f20-186">Para incluir la **URL del Servicio de consumidor de aserciones** en la petición SAML, seleccione **Include Assertion Consumer Service URL** (Incluir URL del Servicio de consumidor de aserciones).</span><span class="sxs-lookup"><span data-stu-id="96f20-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="96f20-187">e.</span><span class="sxs-lookup"><span data-stu-id="96f20-187">e.</span></span> <span data-ttu-id="96f20-188">Haga clic en **Activate Single Sign-On**(Activar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="96f20-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="96f20-189">f.</span><span class="sxs-lookup"><span data-stu-id="96f20-189">f.</span></span> <span data-ttu-id="96f20-190">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="96f20-190">Save your changes.</span></span>
   
    <span data-ttu-id="96f20-191">g.</span><span class="sxs-lookup"><span data-stu-id="96f20-191">g.</span></span> <span data-ttu-id="96f20-192">Haga clic en la pestaña **My System** (Mi sistema).</span><span class="sxs-lookup"><span data-stu-id="96f20-192">Click the **My System** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="96f20-194">h.</span><span class="sxs-lookup"><span data-stu-id="96f20-194">h.</span></span> <span data-ttu-id="96f20-195">Pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en el cuadro de texto **Azure AD Sign On URL** (Dirección URL de inicio de sesión único de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96f20-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="96f20-197">i.</span><span class="sxs-lookup"><span data-stu-id="96f20-197">i.</span></span> <span data-ttu-id="96f20-198">Especifique si el empleado puede elegir manualmente entre iniciar sesión con el id. de usuario y una contraseña o con SSO, para lo que necesita seleccionar **Manual Identity Provider Selection** (Selección manual de proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="96f20-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="96f20-199">j.</span><span class="sxs-lookup"><span data-stu-id="96f20-199">j.</span></span> <span data-ttu-id="96f20-200">En la sección **SSO URL** (URL de SSO), especifique la dirección URL que debe utilizar el empleado para iniciar sesión en el sistema.</span><span class="sxs-lookup"><span data-stu-id="96f20-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="96f20-201">En la lista desplegable URL Sent to Employee (URL que se envía a empleado), puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="96f20-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="96f20-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="96f20-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="96f20-203">El sistema solo envía la dirección URL del sistema normal al empleado.</span><span class="sxs-lookup"><span data-stu-id="96f20-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="96f20-204">El empleado no puede iniciar sesión mediante SSO y debe usar una contraseña o un certificado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="96f20-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="96f20-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="96f20-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="96f20-206">El sistema solo envía la dirección URL de SSO al empleado.</span><span class="sxs-lookup"><span data-stu-id="96f20-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="96f20-207">El empleado puede iniciar sesión mediante SSO.</span><span class="sxs-lookup"><span data-stu-id="96f20-207">The employee can log on using SSO.</span></span> <span data-ttu-id="96f20-208">La solicitud de autenticación se redirige a través de IdP.</span><span class="sxs-lookup"><span data-stu-id="96f20-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="96f20-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="96f20-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="96f20-210">SI SSO no está activo, el sistema envía la dirección URL del sistema normal al empleado.</span><span class="sxs-lookup"><span data-stu-id="96f20-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="96f20-211">Si SSO está activo, el sistema comprueba si el empleado tiene contraseña.</span><span class="sxs-lookup"><span data-stu-id="96f20-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="96f20-212">Si existe una contraseña, se envían al empleado tanto la URL de SSO como la URL no de SSO.</span><span class="sxs-lookup"><span data-stu-id="96f20-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="96f20-213">Sin embargo, si el empleado no tiene contraseña, solo se envía la primera al empleado.</span><span class="sxs-lookup"><span data-stu-id="96f20-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="96f20-214">k.</span><span class="sxs-lookup"><span data-stu-id="96f20-214">k.</span></span> <span data-ttu-id="96f20-215">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="96f20-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="96f20-216">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96f20-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96f20-217">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="96f20-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96f20-218">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96f20-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="96f20-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-219">Create an Azure AD test user</span></span>

<span data-ttu-id="96f20-220">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96f20-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="96f20-222">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="96f20-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96f20-223">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96f20-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="96f20-225">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="96f20-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="96f20-227">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="96f20-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="96f20-229">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="96f20-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="96f20-231">a.</span><span class="sxs-lookup"><span data-stu-id="96f20-231">a.</span></span> <span data-ttu-id="96f20-232">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96f20-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96f20-233">b.</span><span class="sxs-lookup"><span data-stu-id="96f20-233">b.</span></span> <span data-ttu-id="96f20-234">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96f20-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="96f20-235">c.</span><span class="sxs-lookup"><span data-stu-id="96f20-235">c.</span></span> <span data-ttu-id="96f20-236">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="96f20-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="96f20-237">d.</span><span class="sxs-lookup"><span data-stu-id="96f20-237">d.</span></span> <span data-ttu-id="96f20-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="96f20-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="96f20-239">Creación de un usuario de prueba de SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="96f20-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="96f20-240">En esta sección, creará un usuario llamado Britta Simon en SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="96f20-241">Trabaje con el [equipo de soporte técnico de SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) para agregar usuarios en la plataforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="96f20-242">Asegúrese de que el valor de NameID coincide con el campo de nombre de usuario de la plataforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="96f20-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f20-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="96f20-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="96f20-246">**Para asignar Britta Simon a SAP Business ByDesign, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="96f20-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="96f20-247">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="96f20-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="96f20-249">En la lista de aplicaciones, seleccione **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="96f20-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Vínculo a SAP Business ByDesign en la lista de aplicaciones](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="96f20-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="96f20-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="96f20-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="96f20-253">Click **Add** button.</span></span> <span data-ttu-id="96f20-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="96f20-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="96f20-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="96f20-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96f20-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="96f20-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96f20-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="96f20-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="96f20-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="96f20-259">Test single sign-on</span></span>

<span data-ttu-id="96f20-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="96f20-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="96f20-261">Al hacer clic en el icono de SAP Business ByDesign en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="96f20-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96f20-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="96f20-262">Additional resources</span></span>

* [<span data-ttu-id="96f20-263">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f20-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96f20-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96f20-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

