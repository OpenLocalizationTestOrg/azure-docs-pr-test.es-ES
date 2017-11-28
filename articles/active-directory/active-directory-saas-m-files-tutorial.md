---
title: "Tutorial: integración de Azure Active Directory con M-Files | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y M-Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="1d857-103">Tutorial: integración de Azure Active Directory con M-Files</span><span class="sxs-lookup"><span data-stu-id="1d857-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="1d857-104">En este tutorial, aprenderá a integrar M-Files con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d857-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d857-105">La integración de M-Files con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1d857-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d857-106">Puede controlar en Azure AD quién tiene acceso a M-Files</span><span class="sxs-lookup"><span data-stu-id="1d857-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="1d857-107">Puede permitir que los usuarios inicien sesión automáticamente en M-Files (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d857-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d857-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1d857-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d857-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d857-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d857-110">Prerequisites</span></span>

<span data-ttu-id="1d857-111">Para configurar la integración de Azure AD con M-Files, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1d857-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="1d857-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d857-113">Una suscripción habilitada para el inicio de sesión único en M-Files</span><span class="sxs-lookup"><span data-stu-id="1d857-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d857-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1d857-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d857-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1d857-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d857-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1d857-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d857-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d857-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d857-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1d857-118">Scenario description</span></span>
<span data-ttu-id="1d857-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1d857-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d857-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1d857-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d857-121">Incorporación de M-Files desde la galería</span><span class="sxs-lookup"><span data-stu-id="1d857-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="1d857-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="1d857-123">Incorporación de M-Files desde la galería</span><span class="sxs-lookup"><span data-stu-id="1d857-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="1d857-124">Para configurar la integración de M-Files en Azure AD, es preciso agregar M-Files desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1d857-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d857-125">**Para agregar M-Files desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1d857-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d857-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d857-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d857-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1d857-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d857-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d857-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1d857-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d857-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1d857-133">En el cuadro de búsqueda, escriba **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="1d857-133">In the search box, type **M-Files**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="1d857-135">En el panel de resultados, seleccione **M-Files** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d857-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d857-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d857-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con M-Files con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d857-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d857-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de M-Files para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d857-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="1d857-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="1d857-141">Para establecer la relación de vínculo, en M-Files, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1d857-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1d857-142">Para configurar y probar el inicio de sesión único de Azure AD con M-Files, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1d857-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d857-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1d857-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d857-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d857-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d857-145">**[Creación de un usuario de prueba de M-Files](#creating-a-m-files-test-user)**: para tener un homólogo de Britta Simon en M-Files que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d857-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d857-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d857-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d857-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1d857-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d857-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d857-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="1d857-150">**Para configurar el inicio de sesión único de Azure AD con M-Files, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1d857-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1d857-151">En Azure Portal, en la página de integración de la aplicación **M-Files**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1d857-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1d857-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1d857-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="1d857-155">En la sección **Dominio y direcciones URL de M-Files**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1d857-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="1d857-157">a.</span><span class="sxs-lookup"><span data-stu-id="1d857-157">a.</span></span> <span data-ttu-id="1d857-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`.</span><span class="sxs-lookup"><span data-stu-id="1d857-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="1d857-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d857-159">b.</span></span> <span data-ttu-id="1d857-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="1d857-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d857-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1d857-161">These values are not real.</span></span> <span data-ttu-id="1d857-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1d857-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1d857-163">Póngase en contacto con el [equipo de soporte técnico de M-Files](mailto:support@m-files.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1d857-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1d857-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1d857-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="1d857-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1d857-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d857-168">Para configurar SSO en su aplicación, póngase en contacto con el [equipo de soporte técnico de M-Files](mailto:support@m-files.com) y proporciónele el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="1d857-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1d857-169">Siga estos pasos si desea configurar SSO para la aplicación de escritorio de archivo M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="1d857-170">Si solo desea configurar SSO para la versión de web de M-Files, no se necesitan pasos adicionales.</span><span class="sxs-lookup"><span data-stu-id="1d857-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="1d857-171">Siga estos pasos para configurar la aplicación de escritorio M-Files para habilitar SSO con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d857-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="1d857-172">Para descargar M-Files, vaya a la página de [descarga de M-Files](https://www.m-files.com/en/download-latest-version).</span><span class="sxs-lookup"><span data-stu-id="1d857-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="1d857-173">Abra la ventana **M-Files Desktop Settings** (Configuración de escritorio de M-Files).</span><span class="sxs-lookup"><span data-stu-id="1d857-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="1d857-174">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1d857-174">Then, click **Add**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="1d857-176">En la ventana **Document Vault Connection Properties** (Propiedades de conexión del almacén de documentos), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1d857-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="1d857-178">En la sección Server (Servidor), escriba los valores como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="1d857-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="1d857-179">a.</span><span class="sxs-lookup"><span data-stu-id="1d857-179">a.</span></span> <span data-ttu-id="1d857-180">En **Name** (Nombre), escriba `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="1d857-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="1d857-181">b.</span><span class="sxs-lookup"><span data-stu-id="1d857-181">b.</span></span> <span data-ttu-id="1d857-182">En **Port Number** (Número de puerto), escriba **4466**.</span><span class="sxs-lookup"><span data-stu-id="1d857-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="1d857-183">c.</span><span class="sxs-lookup"><span data-stu-id="1d857-183">c.</span></span> <span data-ttu-id="1d857-184">En **Protocol** (Protocolo), seleccione **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="1d857-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="1d857-185">d.</span><span class="sxs-lookup"><span data-stu-id="1d857-185">d.</span></span> <span data-ttu-id="1d857-186">En el campo **Authentication** (Autenticación), seleccione **Specific Windows user** (Usuario específico de Windows).</span><span class="sxs-lookup"><span data-stu-id="1d857-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="1d857-187">Luego, se le solicitará una página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1d857-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="1d857-188">Escriba sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d857-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="1d857-189">e.</span><span class="sxs-lookup"><span data-stu-id="1d857-189">e.</span></span> <span data-ttu-id="1d857-190">En **Vault on Server** (Almacén en servidor),  seleccione el almacén correspondiente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="1d857-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="1d857-191">f.</span><span class="sxs-lookup"><span data-stu-id="1d857-191">f.</span></span> <span data-ttu-id="1d857-192">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1d857-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="1d857-193">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d857-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d857-194">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1d857-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d857-195">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d857-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d857-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d857-197">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d857-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1d857-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1d857-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d857-200">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d857-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d857-202">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1d857-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d857-204">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d857-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d857-206">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1d857-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d857-208">a.</span><span class="sxs-lookup"><span data-stu-id="1d857-208">a.</span></span> <span data-ttu-id="1d857-209">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d857-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d857-210">b.</span><span class="sxs-lookup"><span data-stu-id="1d857-210">b.</span></span> <span data-ttu-id="1d857-211">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d857-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d857-212">c.</span><span class="sxs-lookup"><span data-stu-id="1d857-212">c.</span></span> <span data-ttu-id="1d857-213">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1d857-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d857-214">d.</span><span class="sxs-lookup"><span data-stu-id="1d857-214">d.</span></span> <span data-ttu-id="1d857-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1d857-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="1d857-216">Creación de un usuario de prueba en M-Files</span><span class="sxs-lookup"><span data-stu-id="1d857-216">Creating a M-Files test user</span></span>

<span data-ttu-id="1d857-217">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="1d857-218">Póngase en contacto con el [equipo de soporte técnico de M-Files](mailto:support@m-files.com) para agregar los usuarios en M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d857-219">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d857-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d857-220">En esta sección, concederá acceso a Britta Simon a M-Files para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d857-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1d857-222">**Para asignar el usuario Britta Simon a M-Files, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1d857-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1d857-223">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d857-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1d857-225">En la lista de aplicaciones, seleccione **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="1d857-225">In the applications list, select **M-Files**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="1d857-227">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d857-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1d857-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1d857-229">Click **Add** button.</span></span> <span data-ttu-id="1d857-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1d857-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1d857-232">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1d857-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d857-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d857-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d857-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1d857-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d857-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1d857-235">Testing single sign-on</span></span>

<span data-ttu-id="1d857-236">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1d857-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1d857-237">Al hacer clic en el icono de M-Files en el panel de acceso, debería iniciar sesión automáticamente en su aplicación M-Files.</span><span class="sxs-lookup"><span data-stu-id="1d857-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d857-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1d857-238">Additional resources</span></span>

* [<span data-ttu-id="1d857-239">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d857-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d857-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1d857-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

