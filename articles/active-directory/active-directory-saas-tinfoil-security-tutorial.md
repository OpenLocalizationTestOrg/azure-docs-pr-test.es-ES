---
title: "Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="6603a-103">Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6603a-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="6603a-104">En este tutorial, aprenderá a integrar TINFOIL SECURITY con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6603a-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6603a-105">Integrar TINFOIL SECURITY con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6603a-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6603a-106">Puede controlar en Azure AD quién tiene acceso a TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="6603a-107">Puede permitir que los usuarios inicien sesión automáticamente en TINFOIL SECURITY (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6603a-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6603a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6603a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6603a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6603a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6603a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6603a-110">Prerequisites</span></span>

<span data-ttu-id="6603a-111">Para configurar la integración de Azure AD con TINFOIL SECURITY, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6603a-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="6603a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6603a-113">Una suscripción habilitada para el inicio de sesión único en TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6603a-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6603a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6603a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6603a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6603a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6603a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6603a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6603a-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6603a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6603a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6603a-118">Scenario description</span></span>
<span data-ttu-id="6603a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6603a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6603a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="6603a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6603a-121">Agregar TINFOIL SECURITY desde la galería</span><span class="sxs-lookup"><span data-stu-id="6603a-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="6603a-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="6603a-123">Agregar TINFOIL SECURITY desde la galería</span><span class="sxs-lookup"><span data-stu-id="6603a-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="6603a-124">Para configurar la integración de TINFOIL SECURITY en Azure AD, debe agregar TINFOIL SECURITY desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="6603a-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6603a-125">**Para agregar TINFOIL SECURITY desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6603a-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6603a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6603a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6603a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6603a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6603a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6603a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6603a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6603a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6603a-133">En el cuadro de búsqueda, escriba **TINFOIL SECURITY**, seleccione **TINFOIL SECURITY** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6603a-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![TINFOIL SECURITY desde la galería](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6603a-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6603a-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con TINFOIL SECURITY con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6603a-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6603a-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TINFOIL SECURITY para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6603a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="6603a-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="6603a-139">Para establecer la relación de vínculo, en TINFOIL SECURITY, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="6603a-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6603a-140">Para configurar y probar el inicio de sesión único de Azure AD con TINFOIL SECURITY, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6603a-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6603a-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="6603a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6603a-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6603a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6603a-143">**[Creación de un usuario de prueba de TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**: para tener un homólogo de Britta Simon en TINFOIL SECURITY que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6603a-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6603a-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6603a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6603a-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6603a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6603a-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6603a-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="6603a-148">**Para configurar el inicio de sesión único de Azure AD con TINFOIL SECURITY, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6603a-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="6603a-149">En Azure Portal, en la página de integración de la aplicación **TINFOIL SECURITY**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6603a-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6603a-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6603a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="6603a-153">En la sección **Dominio y direcciones URL de TINFOIL SECURITY**, el usuario no tiene que realizar ningún paso, ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="6603a-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="6603a-155">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL**.</span><span class="sxs-lookup"><span data-stu-id="6603a-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="6603a-157">Para agregar las asignaciones de los atributos necesarios, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6603a-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="6603a-158">![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="6603a-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="6603a-159">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="6603a-159">Attribute Name</span></span>    |   <span data-ttu-id="6603a-160">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="6603a-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="6603a-161">accountid</span><span class="sxs-lookup"><span data-stu-id="6603a-161">accountid</span></span> | <span data-ttu-id="6603a-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="6603a-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="6603a-163">a.</span><span class="sxs-lookup"><span data-stu-id="6603a-163">a.</span></span> <span data-ttu-id="6603a-164">Haga clic en **agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="6603a-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="6603a-165">![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="6603a-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="6603a-166">![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="6603a-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="6603a-167">b.</span><span class="sxs-lookup"><span data-stu-id="6603a-167">b.</span></span> <span data-ttu-id="6603a-168">En el cuadro de texto **Nombre de atributo**, escriba **accountid**.</span><span class="sxs-lookup"><span data-stu-id="6603a-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="6603a-169">c.</span><span class="sxs-lookup"><span data-stu-id="6603a-169">c.</span></span> <span data-ttu-id="6603a-170">En el cuadro de texto **Valor de atributo**, pegue el valor del identificador de cuenta que obtendrá más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="6603a-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="6603a-171">d.</span><span class="sxs-lookup"><span data-stu-id="6603a-171">d.</span></span> <span data-ttu-id="6603a-172">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6603a-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="6603a-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6603a-173">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6603a-175">En la sección **Configuración de TINFOIL SECURITY**, haga clic en **Configurar TINFOIL SECURITY** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6603a-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6603a-176">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="6603a-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="6603a-178">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="6603a-179">En la barra de herramientas de la parte superior, haga clic en el icono de **Mi cuenta**.</span><span class="sxs-lookup"><span data-stu-id="6603a-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="6603a-180">![Panel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Panel")</span><span class="sxs-lookup"><span data-stu-id="6603a-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="6603a-181">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="6603a-181">Click **Security**.</span></span>
   
    <span data-ttu-id="6603a-182">![Seguridad](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="6603a-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="6603a-183">Siga estos pasos en la página de configuración **Inicio de sesión único** :</span><span class="sxs-lookup"><span data-stu-id="6603a-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="6603a-184">![Inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6603a-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="6603a-185">a.</span><span class="sxs-lookup"><span data-stu-id="6603a-185">a.</span></span> <span data-ttu-id="6603a-186">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="6603a-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="6603a-187">b.</span><span class="sxs-lookup"><span data-stu-id="6603a-187">b.</span></span> <span data-ttu-id="6603a-188">Haga clic en **Configuración manual**.</span><span class="sxs-lookup"><span data-stu-id="6603a-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="6603a-189">c.</span><span class="sxs-lookup"><span data-stu-id="6603a-189">c.</span></span> <span data-ttu-id="6603a-190">En el cuadro de texto **SAML Post URL** (Dirección URL de publicación de SAML), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6603a-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="6603a-191">d.</span><span class="sxs-lookup"><span data-stu-id="6603a-191">d.</span></span> <span data-ttu-id="6603a-192">En el cuadro de texto **SAML Certificate Fingerprint** (Huella digital de certificado de SAML), pegue el valor de **Huella digital** del certificado que haya copiado de la sección **Certificado de firma de SAML**.</span><span class="sxs-lookup"><span data-stu-id="6603a-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="6603a-193">e.</span><span class="sxs-lookup"><span data-stu-id="6603a-193">e.</span></span> <span data-ttu-id="6603a-194">Copie el valor del **identificador de la cuenta** y péguelo en el cuadro de texto **Valor de atributo** de la sección **Agregar atributo** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6603a-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="6603a-195">f.</span><span class="sxs-lookup"><span data-stu-id="6603a-195">f.</span></span> <span data-ttu-id="6603a-196">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6603a-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6603a-197">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6603a-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6603a-198">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6603a-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6603a-199">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6603a-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6603a-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-200">Create an Azure AD test user</span></span>
<span data-ttu-id="6603a-201">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6603a-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6603a-203">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6603a-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6603a-204">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6603a-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6603a-206">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6603a-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="6603a-207">Usuarios y grupos -> Todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="6603a-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6603a-208">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6603a-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Usuario](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6603a-210">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6603a-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6603a-212">a.</span><span class="sxs-lookup"><span data-stu-id="6603a-212">a.</span></span> <span data-ttu-id="6603a-213">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6603a-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6603a-214">b.</span><span class="sxs-lookup"><span data-stu-id="6603a-214">b.</span></span> <span data-ttu-id="6603a-215">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6603a-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6603a-216">c.</span><span class="sxs-lookup"><span data-stu-id="6603a-216">c.</span></span> <span data-ttu-id="6603a-217">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6603a-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6603a-218">d.</span><span class="sxs-lookup"><span data-stu-id="6603a-218">d.</span></span> <span data-ttu-id="6603a-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6603a-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="6603a-220">Creación de un usuario de prueba de TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6603a-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="6603a-221">Para permitir que los usuarios de Azure AD inicien sesión en TINFOIL SECURITY, deben aprovisionarse en TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="6603a-222">En el caso de TINFOIL SECURITY, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="6603a-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="6603a-223">**Siga estos pasos para que se aprovisione un usuario:**</span><span class="sxs-lookup"><span data-stu-id="6603a-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="6603a-224">Si el usuario forma parte de una cuenta de empresa, deberá [ponerse en contacto con el equipo de soporte técnico de TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) para que se cree la cuenta del usuario.</span><span class="sxs-lookup"><span data-stu-id="6603a-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="6603a-225">Si el usuario es usuario habitual de SaaS de TINFOIL SECURITY, puede agregar un colaborador a cualquiera de sus sitios.</span><span class="sxs-lookup"><span data-stu-id="6603a-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="6603a-226">Esta acción desencadena un proceso para enviar una invitación al correo electrónico especificado y crear una cuenta de usuario de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="6603a-227">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TINFOIL SECURITY que ofrezca TINFOIL SECURITY para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6603a-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6603a-228">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6603a-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="6603a-229">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6603a-231">**Para asignar Britta Simon a TINFOIL SECURITY, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6603a-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="6603a-232">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6603a-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6603a-234">En la lista de aplicaciones, seleccione **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="6603a-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![Selección de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="6603a-236">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6603a-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6603a-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6603a-238">Click **Add** button.</span></span> <span data-ttu-id="6603a-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6603a-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6603a-241">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6603a-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6603a-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6603a-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6603a-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6603a-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6603a-244">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="6603a-244">Test single sign-on</span></span>

<span data-ttu-id="6603a-245">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6603a-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6603a-246">Al hacer clic en el icono de TINFOIL SECURITY en el panel de acceso, debería iniciar sesión automáticamente en la aplicación TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6603a-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="6603a-247">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6603a-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6603a-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6603a-248">Additional resources</span></span>

* [<span data-ttu-id="6603a-249">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6603a-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6603a-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6603a-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

