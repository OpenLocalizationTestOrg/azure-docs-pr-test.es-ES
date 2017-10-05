---
title: "Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y MOVEit Transfer - Azure AD integration."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="07f63-103">Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="07f63-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="07f63-104">En este tutorial, obtendrá información sobre cómo integrar MOVEit Transfer - Azure AD integration con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07f63-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07f63-105">La integración de MOVEit Transfer - Azure AD integration con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="07f63-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07f63-106">Puede controlar en Azure AD quién tiene acceso a MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="07f63-107">Puede habilitar que los usuarios inicien sesión automáticamente en MOVEit Transfer - Azure AD integration (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07f63-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07f63-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07f63-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="07f63-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07f63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07f63-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07f63-110">Prerequisites</span></span>

<span data-ttu-id="07f63-111">Para configurar la integración de Azure AD con MOVEit Transfer - Azure AD integration, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="07f63-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="07f63-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07f63-113">Una suscripción habilitada para el inicio de sesión único en MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="07f63-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07f63-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="07f63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07f63-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="07f63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07f63-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="07f63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07f63-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07f63-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07f63-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="07f63-118">Scenario description</span></span>
<span data-ttu-id="07f63-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="07f63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07f63-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="07f63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07f63-121">Agregación de MOVEit Transfer - Azure AD integration desde la galería</span><span class="sxs-lookup"><span data-stu-id="07f63-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="07f63-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="07f63-123">Agregación de MOVEit Transfer - Azure AD integration desde la galería</span><span class="sxs-lookup"><span data-stu-id="07f63-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="07f63-124">Para configurar la integración de MOVEit Transfer - Azure AD integration en Azure AD, deberá agregar MOVEit Transfer - Azure AD integration desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="07f63-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07f63-125">**Para agregar MOVEit Transfer - Azure AD integration desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07f63-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07f63-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07f63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="07f63-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="07f63-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07f63-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07f63-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="07f63-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07f63-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="07f63-133">En el cuadro de búsqueda, escriba **MOVEit Transfer - Azure AD integration**, seleccione **MOVEit Transfer - Azure AD integration** en el panel de resultados y, a continuación, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07f63-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer - Azure AD integration en la lista de resultados](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07f63-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="07f63-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con MOVEit Transfer - Azure AD integration con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07f63-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07f63-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de MOVEit Transfer - Azure AD integration para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07f63-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="07f63-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="07f63-139">Para establecer la relación de vínculo, en MOVEit Transfer - Azure AD integration, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="07f63-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07f63-140">Para configurar y probar el inicio de sesión único de Azure AD con MOVEit Transfer - Azure AD integration, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="07f63-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07f63-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="07f63-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07f63-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07f63-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07f63-143">**[Creación de un usuario de prueba en MOVEit Transfer - Azure AD integration](#create-a-moveit-transfer---azure-ad-integration-test-user)**: para tener un homólogo de Britta Simon en MOVEit Transfer - Azure AD integration que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07f63-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07f63-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07f63-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07f63-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="07f63-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07f63-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="07f63-147">En esta sección, se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="07f63-148">**Para configurar el inicio de sesión único de Azure AD con MOVEit Transfer - Azure AD integration, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07f63-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="07f63-149">En la página de integración de la aplicación **MOVEit Transfer - Azure AD integration** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="07f63-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="07f63-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="07f63-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="07f63-153">En la sección **Dominio y direcciones URL de MOVEit Transfer - Azure AD integration** realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="07f63-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="07f63-155">a.</span><span class="sxs-lookup"><span data-stu-id="07f63-155">a.</span></span> <span data-ttu-id="07f63-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="07f63-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="07f63-157">b.</span><span class="sxs-lookup"><span data-stu-id="07f63-157">b.</span></span> <span data-ttu-id="07f63-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="07f63-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="07f63-159">c.</span><span class="sxs-lookup"><span data-stu-id="07f63-159">c.</span></span> <span data-ttu-id="07f63-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`.</span><span class="sxs-lookup"><span data-stu-id="07f63-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="07f63-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="07f63-161">These values are not real.</span></span> <span data-ttu-id="07f63-162">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="07f63-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="07f63-163">Puede hacer referencia a estos valores más tarde en la sección **Dirección URL de metadatos del proveedor de servicios** o póngase en contacto con el [equipo de soporte técnico de MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="07f63-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="07f63-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="07f63-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="07f63-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="07f63-166">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="07f63-168">Inicie la sesión en el inquilino de MOVEit Transfer como administrador.</span><span class="sxs-lookup"><span data-stu-id="07f63-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="07f63-169">En la barra de navegación de la izquierda, haga clic en **Settings**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="07f63-169">On the left navigation pane, click **Settings**.</span></span>

    ![Sección Configuración en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="07f63-171">Haga clic en el vínculo **Single Signon** (Inicio de sesión único) que se encuentra en **Security Policies -> User Auth** (Directivas de seguridad -> Autenticación de usuario).</span><span class="sxs-lookup"><span data-stu-id="07f63-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Directivas de seguridad en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="07f63-173">Haga clic en el vínculo Metadata URL (Dirección URL de metadatos) para descargar el documento de metadatos.</span><span class="sxs-lookup"><span data-stu-id="07f63-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![Dirección URL de metadatos del proveedor de servicios](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="07f63-175">Compruebe que **entityID** (identificador de entidad) coincide con **Identifier** (identificador) en la sección **Dominio y direcciones URL de MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="07f63-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="07f63-176">Compruebe que la dirección URL de la ubicación de **AssertionConsumerService** coincide con **REPLY URL** (dirección URL de respuesta) en la sección **Dominio y direcciones URL de MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="07f63-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="07f63-178">Haga clic en el botón **Add Identity Provider** (Agregar proveedor de identidades) para agregar un nuevo proveedor de identidad federada.</span><span class="sxs-lookup"><span data-stu-id="07f63-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Agregación del proveedor de identidades](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="07f63-180">Haga clic en **Browse...** (Examinar...) para seleccionar el archivo de metadatos que descargó de Azure Portal y, después, haga clic en **Add Identity Provider** (Agregar proveedor de identidades) para cargar el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="07f63-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![Proveedor de identidades de SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="07f63-182">Seleccione "**Yes**" (Sí) en la opción **Enabled** (Habilitado) de la página **Edit Federated Identity Provider Settings** (Editar configuración de proveedor de identidades federada) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="07f63-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="07f63-184">En la página **Edit Federated Identity Provider Settings** (Editar configuración del proveedor de identidades federadas), realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="07f63-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Edición de la configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="07f63-186">a.</span><span class="sxs-lookup"><span data-stu-id="07f63-186">a.</span></span> <span data-ttu-id="07f63-187">Seleccione **SAML NameID** en **Login name** (Nombre de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="07f63-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="07f63-188">b.</span><span class="sxs-lookup"><span data-stu-id="07f63-188">b.</span></span> <span data-ttu-id="07f63-189">Seleccione **Other** (Otros) como **Full name** (Nombre completo) y en el cuadro de texto **Attribute name** (Nombre de atributo) coloque el valor: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="07f63-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="07f63-190">c.</span><span class="sxs-lookup"><span data-stu-id="07f63-190">c.</span></span> <span data-ttu-id="07f63-191">Seleccione **Other** (Otros) como **Email** (Correo electrónico) y en el cuadro de texto **Attribute name** (Nombre de atributo) coloque el valor: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="07f63-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="07f63-192">d.</span><span class="sxs-lookup"><span data-stu-id="07f63-192">d.</span></span> <span data-ttu-id="07f63-193">Seleccione **Yes** (Sí) en **Auto-create account on signon** (Crear automáticamente cuenta al iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="07f63-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="07f63-194">e.</span><span class="sxs-lookup"><span data-stu-id="07f63-194">e.</span></span> <span data-ttu-id="07f63-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="07f63-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="07f63-196">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07f63-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07f63-197">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="07f63-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07f63-198">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07f63-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07f63-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-199">Create an Azure AD test user</span></span>

<span data-ttu-id="07f63-200">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07f63-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="07f63-202">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="07f63-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07f63-203">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07f63-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="07f63-205">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="07f63-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="07f63-207">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="07f63-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="07f63-209">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07f63-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="07f63-211">a.</span><span class="sxs-lookup"><span data-stu-id="07f63-211">a.</span></span> <span data-ttu-id="07f63-212">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07f63-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07f63-213">b.</span><span class="sxs-lookup"><span data-stu-id="07f63-213">b.</span></span> <span data-ttu-id="07f63-214">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07f63-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="07f63-215">c.</span><span class="sxs-lookup"><span data-stu-id="07f63-215">c.</span></span> <span data-ttu-id="07f63-216">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="07f63-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="07f63-217">d.</span><span class="sxs-lookup"><span data-stu-id="07f63-217">d.</span></span> <span data-ttu-id="07f63-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="07f63-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="07f63-219">Creación de un usuario de prueba de MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="07f63-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="07f63-220">El objetivo de esta sección es crear un usuario llamado Britta Simon en MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="07f63-221">MOVEit Transfer - Azure AD integration admite el aprovisionamiento Just-In-Time que ha habilitado.</span><span class="sxs-lookup"><span data-stu-id="07f63-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="07f63-222">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="07f63-222">There is no action item for you in this section.</span></span> <span data-ttu-id="07f63-223">Al intentar acceder a MOVEit Transfer - Azure AD integration se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="07f63-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="07f63-224">Si necesita crear un usuario manualmente, es preciso que se ponga en contacto con el [equipo de soporte técnico de MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="07f63-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="07f63-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07f63-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="07f63-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="07f63-228">**Para asignar a Britta Simon a MOVEit Transfer - Azure AD integration, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07f63-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="07f63-229">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07f63-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="07f63-231">En la lista de aplicaciones, seleccione **MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="07f63-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Vínculo a MOVEit Transfer - Azure AD integration en la lista de aplicaciones](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="07f63-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07f63-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="07f63-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="07f63-235">Click **Add** button.</span></span> <span data-ttu-id="07f63-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07f63-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="07f63-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="07f63-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07f63-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07f63-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07f63-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07f63-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="07f63-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="07f63-241">Test single sign-on</span></span>

<span data-ttu-id="07f63-242">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="07f63-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="07f63-243">Al hacer clic en el icono de MOVEit Transfer - Azure AD integration en el panel de acceso, debería iniciar sesión automáticamente en la aplicación MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="07f63-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="07f63-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="07f63-244">Additional resources</span></span>

* [<span data-ttu-id="07f63-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07f63-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07f63-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07f63-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

