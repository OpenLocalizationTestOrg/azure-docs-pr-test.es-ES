---
title: "Tutorial: Integración de Azure Active Directory con Workstars | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: e17c85689fa3aebf00ebf559185032b90103b4a5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="ad45b-103">Tutorial: integración de Azure Active Directory con Workstars</span><span class="sxs-lookup"><span data-stu-id="ad45b-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="ad45b-104">En este tutorial, obtendrá información sobre cómo integrar Workstars con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad45b-104">In this tutorial, you learn how to integrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad45b-105">La integración de Workstars con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ad45b-105">Integrating Workstars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad45b-106">Puede controlar en Azure AD quién tiene acceso a Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-106">You can control in Azure AD who has access to Workstars.</span></span>
- <span data-ttu-id="ad45b-107">Puede permitir que los usuarios inicien sesión automáticamente en Workstars (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad45b-107">You can enable your users to automatically get signed-on to Workstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ad45b-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ad45b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ad45b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad45b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad45b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ad45b-110">Prerequisites</span></span>

<span data-ttu-id="ad45b-111">Para configurar la integración de Azure AD con Workstars, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ad45b-111">To configure Azure AD integration with Workstars, you need the following items:</span></span>

- <span data-ttu-id="ad45b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad45b-113">Una suscripción habilitada para el inicio de sesión único en Workstars</span><span class="sxs-lookup"><span data-stu-id="ad45b-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad45b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ad45b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad45b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ad45b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad45b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ad45b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad45b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad45b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad45b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ad45b-118">Scenario description</span></span>
<span data-ttu-id="ad45b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ad45b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad45b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ad45b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad45b-121">Agregar Workstars desde la galería</span><span class="sxs-lookup"><span data-stu-id="ad45b-121">Adding Workstars from the gallery</span></span>
2. <span data-ttu-id="ad45b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-the-gallery"></a><span data-ttu-id="ad45b-123">Agregar Workstars desde la galería</span><span class="sxs-lookup"><span data-stu-id="ad45b-123">Adding Workstars from the gallery</span></span>
<span data-ttu-id="ad45b-124">Para configurar la integración de Workstars en Azure AD, será preciso que agregue Workstars desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ad45b-124">To configure the integration of Workstars into Azure AD, you need to add Workstars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad45b-125">**Para agregar Workstars desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ad45b-125">**To add Workstars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad45b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="ad45b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad45b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="ad45b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad45b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="ad45b-133">En el cuadro de búsqueda, escriba **Workstars**, seleccione **Workstars** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad45b-133">In the search box, type **Workstars**, select **Workstars** from result panel then click **Add** button to add the application.</span></span>

    ![Workstars en la lista de resultados](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ad45b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ad45b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workstars con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad45b-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad45b-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workstars para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad45b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workstars is to a user in Azure AD.</span></span> <span data-ttu-id="ad45b-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-138">In other words, a link relationship between an Azure AD user and the related user in Workstars needs to be established.</span></span>

<span data-ttu-id="ad45b-139">Para establecer la relación de vínculo, en Workstars, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-139">In Workstars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ad45b-140">Para configurar y probar el inicio de sesión único de Azure AD con Workstars, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ad45b-140">To configure and test Azure AD single sign-on with Workstars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad45b-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="ad45b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ad45b-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad45b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad45b-143">**[Creación de un usuario de prueba de Workstars](#create-a-workstars-test-user)**: para tener un homólogo de Britta Simon en Workstars que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad45b-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - to have a counterpart of Britta Simon in Workstars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad45b-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad45b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad45b-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="ad45b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ad45b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ad45b-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="ad45b-148">**Para configurar el inicio de sesión único de Azure AD con Workstars, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ad45b-148">**To configure Azure AD single sign-on with Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="ad45b-149">En Azure Portal, en la página de integración de la aplicación **Workstars**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-149">In the Azure portal, on the **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="ad45b-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ad45b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="ad45b-153">En la sección **Dominio y direcciones URL de Workstars**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad45b-153">On the **Workstars Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="ad45b-155">a.</span><span class="sxs-lookup"><span data-stu-id="ad45b-155">a.</span></span> <span data-ttu-id="ad45b-156">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="ad45b-156">In the **Identifier** textbox, type the URL: `https://workstars.com`</span></span>

    <span data-ttu-id="ad45b-157">b.</span><span class="sxs-lookup"><span data-stu-id="ad45b-157">b.</span></span> <span data-ttu-id="ad45b-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.workstars.com/saml/login_check`.</span><span class="sxs-lookup"><span data-stu-id="ad45b-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad45b-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="ad45b-159">The value is not real.</span></span> <span data-ttu-id="ad45b-160">Actualícelo con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="ad45b-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="ad45b-161">Póngase en contacto con el [equipo de soporte técnico de Workstars](https://support.workstars.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="ad45b-161">Contact [Workstars support team](https://support.workstars.com) to get the value.</span></span>
 
4. <span data-ttu-id="ad45b-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ad45b-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="ad45b-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ad45b-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad45b-166">En la sección **Configuración de Workstars**, haga clic en **Configurar Workstars** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-166">On the **Workstars Configuration** section, click **Configure Workstars** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ad45b-167">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="ad45b-169">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Workstars como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad45b-169">In another browser window, sign on to your Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="ad45b-170">En la barra de herramientas principal, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-170">In the main toolbar, click **Settings**.</span></span>

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="ad45b-172">Vaya a **Iniciar sesión** > **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-172">Go to **Sign On** > **Settings**.</span></span>

    ![Inicio de sesión de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="ad45b-175">En la página **Configuración de inicio de sesión único (SAML)** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ad45b-175">On the **Single Sign On (SAML) - Settings** page, perform the following steps:</span></span>
    
    ![SAML de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="ad45b-177">a.</span><span class="sxs-lookup"><span data-stu-id="ad45b-177">a.</span></span> <span data-ttu-id="ad45b-178">En el cuadro de texto **Nombre del proveedor de identidad**, escriba **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="ad45b-179">b.</span><span class="sxs-lookup"><span data-stu-id="ad45b-179">b.</span></span> <span data-ttu-id="ad45b-180">En el cuadro de texto **Identity Provider Entity ID)** (Identificador de entidad del proveedor de identidad), pegue el valor del **Identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ad45b-180">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ad45b-181">c.</span><span class="sxs-lookup"><span data-stu-id="ad45b-181">c.</span></span> <span data-ttu-id="ad45b-182">Copie el contenido del archivo del certificado descargado en el Bloc de notas y luego péguelo en el cuadro de texto **Certificado x509**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-182">Copy the content of the downloaded certificate file in notepad, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="ad45b-183">d.</span><span class="sxs-lookup"><span data-stu-id="ad45b-183">d.</span></span> <span data-ttu-id="ad45b-184">En el cuadro de texto **SAML SSO URL** (Dirección URL de inicio de sesión único de SAML), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ad45b-184">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ad45b-185">e.</span><span class="sxs-lookup"><span data-stu-id="ad45b-185">e.</span></span> <span data-ttu-id="ad45b-186">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión remoto), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ad45b-186">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ad45b-187">f.</span><span class="sxs-lookup"><span data-stu-id="ad45b-187">f.</span></span> <span data-ttu-id="ad45b-188">Seleccione **Id. de nombre** como **Correo electrónico (predeterminado)**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="ad45b-189">g.</span><span class="sxs-lookup"><span data-stu-id="ad45b-189">g.</span></span> <span data-ttu-id="ad45b-190">Haga clic en **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="ad45b-191">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad45b-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ad45b-192">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ad45b-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ad45b-193">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad45b-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ad45b-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-194">Create an Azure AD test user</span></span>

<span data-ttu-id="ad45b-195">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad45b-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="ad45b-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ad45b-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad45b-198">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ad45b-200">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ad45b-202">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ad45b-204">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad45b-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ad45b-206">a.</span><span class="sxs-lookup"><span data-stu-id="ad45b-206">a.</span></span> <span data-ttu-id="ad45b-207">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad45b-208">b.</span><span class="sxs-lookup"><span data-stu-id="ad45b-208">b.</span></span> <span data-ttu-id="ad45b-209">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad45b-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ad45b-210">c.</span><span class="sxs-lookup"><span data-stu-id="ad45b-210">c.</span></span> <span data-ttu-id="ad45b-211">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ad45b-212">d.</span><span class="sxs-lookup"><span data-stu-id="ad45b-212">d.</span></span> <span data-ttu-id="ad45b-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="ad45b-214">Creación de un usuario de prueba de Workstars</span><span class="sxs-lookup"><span data-stu-id="ad45b-214">Create a Workstars test user</span></span>

<span data-ttu-id="ad45b-215">En esta sección, se crea un usuario denominado Britta Simon en Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="ad45b-216">Trabaje con el [equipo de soporte técnico de Workstars](https://support.workstars.com) para agregar los usuarios a la plataforma de Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-216">Work with [Workstars support team](https://support.workstars.com) to add the users in the Workstars platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ad45b-217">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad45b-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="ad45b-218">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workstars.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="ad45b-220">**Para asignar a Britta Simon a Workstars, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad45b-220">**To assign Britta Simon to Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="ad45b-221">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ad45b-223">En la lista de aplicaciones, seleccione **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-223">In the applications list, select **Workstars**.</span></span>

    ![Vínculo a Workstars en la lista de aplicaciones](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="ad45b-225">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="ad45b-227">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-227">Click **Add** button.</span></span> <span data-ttu-id="ad45b-228">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="ad45b-230">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ad45b-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ad45b-231">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad45b-232">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ad45b-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ad45b-233">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ad45b-233">Test single sign-on</span></span>

<span data-ttu-id="ad45b-234">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ad45b-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ad45b-235">Al hacer clic en el icono de Workstars en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Workstars.</span><span class="sxs-lookup"><span data-stu-id="ad45b-235">When you click the Workstars tile in the Access Panel, you should get automatically signed-on to your Workstars application.</span></span>
<span data-ttu-id="ad45b-236">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad45b-236">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ad45b-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ad45b-237">Additional resources</span></span>

* [<span data-ttu-id="ad45b-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad45b-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad45b-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad45b-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

