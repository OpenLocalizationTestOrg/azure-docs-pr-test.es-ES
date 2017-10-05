---
title: "Tutorial: Integración de Azure Active Directory con Citrix ShareFile | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="6ed08-103">Tutorial: Integración de Azure Active Directory con Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6ed08-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="6ed08-104">En este tutorial, aprenderá a integrar Citrix ShareFile con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ed08-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ed08-105">La integración de Citrix ShareFile con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6ed08-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ed08-106">En Azure AD puede controlar quién tiene acceso a Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="6ed08-107">Puede permitir que los usuarios inicien sesión automáticamente en Citrix ShareFile (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed08-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6ed08-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ed08-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6ed08-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ed08-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ed08-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6ed08-110">Prerequisites</span></span>

<span data-ttu-id="6ed08-111">Para configurar la integración de Azure AD con Citrix ShareFile, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6ed08-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="6ed08-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ed08-113">Una suscripción habilitada para el inicio de sesión único en Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6ed08-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ed08-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6ed08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ed08-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6ed08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ed08-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6ed08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ed08-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ed08-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ed08-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6ed08-118">Scenario description</span></span>
<span data-ttu-id="6ed08-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6ed08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ed08-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="6ed08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ed08-121">Incorporación de Citrix ShareFile desde la galería</span><span class="sxs-lookup"><span data-stu-id="6ed08-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="6ed08-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="6ed08-123">Incorporación de Citrix ShareFile desde la galería</span><span class="sxs-lookup"><span data-stu-id="6ed08-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="6ed08-124">Para configurar la integración de Citrix ShareFile en Azure AD, deberá agregar Citrix ShareFile desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="6ed08-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ed08-125">**Para agregar Citrix ShareFile desde la galería, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="6ed08-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ed08-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="6ed08-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ed08-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="6ed08-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ed08-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="6ed08-133">En el cuadro de búsqueda, escriba **Citrix ShareFile**, seleccione **Citrix ShareFile** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ed08-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile en la lista de resultados](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6ed08-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6ed08-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Citrix ShareFile con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6ed08-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ed08-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en Citrix ShareFile de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed08-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="6ed08-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="6ed08-139">Para establecer la relación de vínculo, en Citrix ShareFile, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ed08-140">Para configurar y probar el inicio de sesión único de Azure AD con Citrix ShareFile, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6ed08-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ed08-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="6ed08-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ed08-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ed08-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ed08-143">**[Creación de un usuario de prueba de Citrix ShareFile ](#create-a-citrix-sharefile-test-user)**: para tener un homólogo de Britta Simon en Citrix ShareFile que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed08-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ed08-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed08-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ed08-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="6ed08-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6ed08-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6ed08-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="6ed08-148">**Para configurar el inicio de sesión único de Azure AD con Citrix ShareFile, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="6ed08-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="6ed08-149">En Azure Portal, en la página de integración de la aplicación **Citrix ShareFile**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="6ed08-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6ed08-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="6ed08-153">En la sección **Dominio y direcciones URL de Citrix ShareFile**, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6ed08-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="6ed08-155">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.sharefile.com/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="6ed08-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ed08-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="6ed08-156">This value is not real.</span></span> <span data-ttu-id="6ed08-157">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="6ed08-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="6ed08-158">Póngase en contacto con el [equipo de soporte técnico de Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="6ed08-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="6ed08-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6ed08-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="6ed08-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6ed08-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ed08-163">En la sección **Configuración de Citrix ShareFile**, haga clic en **Configurar Citrix ShareFile** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ed08-164">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="6ed08-166">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="6ed08-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="6ed08-167">En la barra de herramientas de la parte superior, haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="6ed08-168">En el panel de navegación izquierdo, haga clic en **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="6ed08-169">![Administración de cuentas](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Administración de cuentas")</span><span class="sxs-lookup"><span data-stu-id="6ed08-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="6ed08-170">En la página del cuadro de diálogo **Configuración de inicio de sesión único/SAML 2.0** en **Configuración básica**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6ed08-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="6ed08-171">![Inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6ed08-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="6ed08-172">a.</span><span class="sxs-lookup"><span data-stu-id="6ed08-172">a.</span></span> <span data-ttu-id="6ed08-173">Haga clic en **Enable SAML**(Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="6ed08-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="6ed08-174">b.</span><span class="sxs-lookup"><span data-stu-id="6ed08-174">b.</span></span> <span data-ttu-id="6ed08-175">En el cuadro de texto **Your IDP Issuer/ Entity ID** (Emisor del IDP/Id. de entidad), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ed08-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6ed08-176">c.</span><span class="sxs-lookup"><span data-stu-id="6ed08-176">c.</span></span> <span data-ttu-id="6ed08-177">Haga clic en **Cambiar** junto al campo **Certificado X.509** y luego cargue el certificado que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ed08-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="6ed08-178">d.</span><span class="sxs-lookup"><span data-stu-id="6ed08-178">d.</span></span> <span data-ttu-id="6ed08-179">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ed08-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6ed08-180">e.</span><span class="sxs-lookup"><span data-stu-id="6ed08-180">e.</span></span> <span data-ttu-id="6ed08-181">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ed08-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="6ed08-182">Haga clic en **Guardar** en el portal de administración de Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="6ed08-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ed08-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ed08-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6ed08-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ed08-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ed08-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6ed08-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-186">Create an Azure AD test user</span></span>

<span data-ttu-id="6ed08-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6ed08-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="6ed08-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6ed08-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ed08-190">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6ed08-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6ed08-194">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6ed08-196">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6ed08-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6ed08-198">a.</span><span class="sxs-lookup"><span data-stu-id="6ed08-198">a.</span></span> <span data-ttu-id="6ed08-199">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ed08-200">b.</span><span class="sxs-lookup"><span data-stu-id="6ed08-200">b.</span></span> <span data-ttu-id="6ed08-201">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ed08-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6ed08-202">c.</span><span class="sxs-lookup"><span data-stu-id="6ed08-202">c.</span></span> <span data-ttu-id="6ed08-203">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6ed08-204">d.</span><span class="sxs-lookup"><span data-stu-id="6ed08-204">d.</span></span> <span data-ttu-id="6ed08-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="6ed08-206">Creación de un usuario de prueba de Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6ed08-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="6ed08-207">Para permitir que los usuarios de Azure AD inicien sesión en Citrix ShareFile, tienen que aprovisionarse en Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="6ed08-208">En el caso de Citrix ShareFile, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="6ed08-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="6ed08-209">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="6ed08-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6ed08-210">Inicie sesión en su inquilino **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="6ed08-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="6ed08-211">Haga clic en **Manage Users \> (Administrar usuarios) Manage Users Home \> (Administrar página de inicio de usuarios) + Create Employee** (Crear empleado).</span><span class="sxs-lookup"><span data-stu-id="6ed08-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="6ed08-212">![Crear empleado](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Crear empleado")</span><span class="sxs-lookup"><span data-stu-id="6ed08-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="6ed08-213">En la sección **Basic Information** (Información básica), siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6ed08-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="6ed08-214">![Información básica](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Información básica")</span><span class="sxs-lookup"><span data-stu-id="6ed08-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="6ed08-215">a.</span><span class="sxs-lookup"><span data-stu-id="6ed08-215">a.</span></span> <span data-ttu-id="6ed08-216">En el cuadro de texto **E-mail Address** (Dirección de correo electrónico), escriba la dirección de correo electrónico de Britta Simon como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="6ed08-217">b.</span><span class="sxs-lookup"><span data-stu-id="6ed08-217">b.</span></span> <span data-ttu-id="6ed08-218">En el cuadro de texto **First name** (Nombre), escriba el **nombre** del usuario, en este caso, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="6ed08-219">c.</span><span class="sxs-lookup"><span data-stu-id="6ed08-219">c.</span></span> <span data-ttu-id="6ed08-220">En el cuadro de texto **Last name** (Apellido), escriba el **apellido** del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="6ed08-221">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="6ed08-222">El titular de la cuenta de Azure AD recibirá un correo electrónico y seguirá un vínculo para confirmar la cuenta antes de que se active. Puede usar cualquier otra herramienta de creación de cuentas de usuario de Citrix ShareFile o API que Citrix ShareFile proporcione para aprovisionar las cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed08-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6ed08-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed08-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="6ed08-224">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure, para lo cual le concederá acceso a Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="6ed08-226">**Para asignar Britta Simon a Citrix ShareFile, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="6ed08-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="6ed08-227">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6ed08-229">En la lista de aplicaciones, seleccione **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Vínculo de Citrix ShareFile en la lista de aplicaciones](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="6ed08-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="6ed08-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-233">Click **Add** button.</span></span> <span data-ttu-id="6ed08-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="6ed08-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6ed08-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ed08-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ed08-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6ed08-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6ed08-239">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="6ed08-239">Test single sign-on</span></span>

<span data-ttu-id="6ed08-240">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6ed08-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ed08-241">Al hacer clic en el icono de Citrix ShareFile en el Panel de acceso, debe iniciar sesión automáticamente en la aplicación Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6ed08-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="6ed08-242">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ed08-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6ed08-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6ed08-243">Additional resources</span></span>

* [<span data-ttu-id="6ed08-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ed08-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ed08-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ed08-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

