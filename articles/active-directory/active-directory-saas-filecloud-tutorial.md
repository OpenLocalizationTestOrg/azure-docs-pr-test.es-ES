---
title: "Tutorial: Integración de Azure Active Directory con FileCloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="e27b6-103">Tutorial: integración de Azure Active Directory con FileCloud</span><span class="sxs-lookup"><span data-stu-id="e27b6-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="e27b6-104">En este tutorial, aprenderá a integrar FileCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e27b6-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e27b6-105">La integración de FileCloud con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e27b6-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e27b6-106">Puede controlar en Azure AD quién tiene acceso a FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="e27b6-107">Puede permitir que los usuarios inicien sesión automáticamente en FileCloud (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b6-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e27b6-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e27b6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e27b6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e27b6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e27b6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e27b6-110">Prerequisites</span></span>

<span data-ttu-id="e27b6-111">Para configurar la integración de Azure AD con FileCloud se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e27b6-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="e27b6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e27b6-113">Una suscripción habilitada para el inicio de sesión único en FileCloud</span><span class="sxs-lookup"><span data-stu-id="e27b6-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e27b6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e27b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e27b6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e27b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e27b6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e27b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e27b6-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e27b6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e27b6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e27b6-118">Scenario description</span></span>
<span data-ttu-id="e27b6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e27b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e27b6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e27b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e27b6-121">Incorporación de FileCloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="e27b6-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="e27b6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="e27b6-123">Incorporación de FileCloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="e27b6-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="e27b6-124">Para configurar la integración de FileCloud en Azure AD, será preciso que agregue FileCloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e27b6-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e27b6-125">**Para agregar FileCloud desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e27b6-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="e27b6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e27b6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="e27b6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e27b6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="e27b6-133">En el cuadro de búsqueda, escriba **FileCloud**, seleccione **FileCloud** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e27b6-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud en la lista de resultados](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e27b6-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e27b6-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FileCloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e27b6-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e27b6-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de FileCloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="e27b6-138">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="e27b6-139">Para establecer la relación de vínculo, en FileCloud, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e27b6-140">Para configurar y probar el inicio de sesión único de Azure AD con FileCloud, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e27b6-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e27b6-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="e27b6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e27b6-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e27b6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e27b6-143">**[Creación de un usuario de prueba de FileCloud](#create-a-filecloud-test-user)**: para tener un homólogo de Britta Simon en FileCloud que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b6-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e27b6-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e27b6-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="e27b6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e27b6-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e27b6-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="e27b6-148">**Para configurar el inicio de sesión único de Azure AD con FileCloud, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e27b6-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b6-149">En Azure Portal, en la página de integración de la aplicación **FileCloud**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="e27b6-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e27b6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="e27b6-153">En la sección **Dominio y direcciones URL de FileCloud**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e27b6-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="e27b6-155">a.</span><span class="sxs-lookup"><span data-stu-id="e27b6-155">a.</span></span> <span data-ttu-id="e27b6-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.filecloudhosted.com`.</span><span class="sxs-lookup"><span data-stu-id="e27b6-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="e27b6-157">b.</span><span class="sxs-lookup"><span data-stu-id="e27b6-157">b.</span></span> <span data-ttu-id="e27b6-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="e27b6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e27b6-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e27b6-159">These values are not real.</span></span> <span data-ttu-id="e27b6-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e27b6-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e27b6-161">Póngase en contacto con el [equipo de soporte técnico de FileCloud](mailto:support@codelathe.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e27b6-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="e27b6-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e27b6-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="e27b6-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e27b6-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e27b6-166">En la sección **Configuración de FileCloud**, haga clic en **Configurar FileCloud** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e27b6-167">Copie el valor de **Identificador de entidad de SAML** de la **sección Referencia rápida**</span><span class="sxs-lookup"><span data-stu-id="e27b6-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuración de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="e27b6-169">En otra ventana del explorador web, inicie sesión en el inquilino de FileCloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="e27b6-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="e27b6-170">En la barra de navegación de la izquierda, haga clic en **Settings**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="e27b6-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Sección Configuración en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="e27b6-172">Haga clic en la ficha **SSO** de la sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="e27b6-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Pestaña Inicio de sesión único en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="e27b6-174">Seleccione **SAML** como **Default SSO Type** (Tipo de SSO predeterminado) en el panel **Configuración de inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Panel de configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="e27b6-176">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **IdP End Point URL** (Dirección URL del punto de conexión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="e27b6-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Cuadro de texto Dirección URL del punto de conexión del IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="e27b6-178">Abra el archivo de metadatos descargado en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **IdP Meta Data** (Metadatos de IdP) en el panel **Configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Sección de metadatos del IDP en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="e27b6-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e27b6-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="e27b6-181">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e27b6-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e27b6-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e27b6-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e27b6-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e27b6-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e27b6-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-184">Create an Azure AD test user</span></span>

<span data-ttu-id="e27b6-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e27b6-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="e27b6-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e27b6-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b6-188">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e27b6-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e27b6-192">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e27b6-194">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e27b6-194">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e27b6-196">a.</span><span class="sxs-lookup"><span data-stu-id="e27b6-196">a.</span></span> <span data-ttu-id="e27b6-197">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e27b6-198">b.</span><span class="sxs-lookup"><span data-stu-id="e27b6-198">b.</span></span> <span data-ttu-id="e27b6-199">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e27b6-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e27b6-200">c.</span><span class="sxs-lookup"><span data-stu-id="e27b6-200">c.</span></span> <span data-ttu-id="e27b6-201">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e27b6-202">d.</span><span class="sxs-lookup"><span data-stu-id="e27b6-202">d.</span></span> <span data-ttu-id="e27b6-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="e27b6-204">Creación de un usuario de prueba de FileCloud</span><span class="sxs-lookup"><span data-stu-id="e27b6-204">Create a FileCloud test user</span></span>

<span data-ttu-id="e27b6-205">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="e27b6-206">FileCloud admite el aprovisionamiento just-in-time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e27b6-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e27b6-207">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="e27b6-207">There is no action item for you in this section.</span></span> <span data-ttu-id="e27b6-208">Durante un intento de acceder a FileCloud se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="e27b6-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e27b6-209">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="e27b6-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e27b6-210">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b6-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="e27b6-211">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="e27b6-213">**Para asignar Britta Simon a FileCloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e27b6-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b6-214">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e27b6-216">En la lista de aplicaciones, seleccione **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-216">In the applications list, select **FileCloud**.</span></span>

    ![Enlace a FileCloud en la lista de aplicaciones](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="e27b6-218">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="e27b6-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-220">Click **Add** button.</span></span> <span data-ttu-id="e27b6-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="e27b6-223">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e27b6-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e27b6-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e27b6-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e27b6-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e27b6-226">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e27b6-226">Test single sign-on</span></span>

<span data-ttu-id="e27b6-227">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e27b6-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e27b6-228">Al hacer clic en el icono de FileCloud en el panel de acceso, debería iniciar sesión automáticamente en la aplicación FileCloud.</span><span class="sxs-lookup"><span data-stu-id="e27b6-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e27b6-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e27b6-229">Additional resources</span></span>

* [<span data-ttu-id="e27b6-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e27b6-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e27b6-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e27b6-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

