---
title: "Tutorial: Integración de Azure Active Directory con Veracode | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="f26e5-103">Tutorial: integración de Azure Active Directory con Veracode</span><span class="sxs-lookup"><span data-stu-id="f26e5-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="f26e5-104">En este tutorial, obtendrá información sobre cómo integrar Veracode con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f26e5-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f26e5-105">La integración de Veracode con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f26e5-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f26e5-106">Puede controlar en Azure AD quién tiene acceso a Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="f26e5-107">Puede permitir que los usuarios inicien sesión automáticamente en Veracode (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26e5-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f26e5-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f26e5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f26e5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f26e5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f26e5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f26e5-110">Prerequisites</span></span>

<span data-ttu-id="f26e5-111">Para configurar la integración de Azure AD con Veracode, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f26e5-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="f26e5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f26e5-113">Una suscripción habilitada para el inicio de sesión único en Veracode</span><span class="sxs-lookup"><span data-stu-id="f26e5-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f26e5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f26e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f26e5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f26e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f26e5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f26e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f26e5-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f26e5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f26e5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f26e5-118">Scenario description</span></span>
<span data-ttu-id="f26e5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f26e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f26e5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f26e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f26e5-121">Agregación de Veracode desde la galería</span><span class="sxs-lookup"><span data-stu-id="f26e5-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="f26e5-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="f26e5-123">Agregación de Veracode desde la galería</span><span class="sxs-lookup"><span data-stu-id="f26e5-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="f26e5-124">Para configurar la integración de Veracode en Azure AD, deberá agregar Veracode desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f26e5-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f26e5-125">**Para agregar Veracode desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f26e5-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f26e5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="f26e5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f26e5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="f26e5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f26e5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="f26e5-133">En el cuadro de búsqueda, escriba **Veracode**, seleccione **Veracode** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f26e5-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode en la lista de resultados](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f26e5-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f26e5-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Veracode con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f26e5-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f26e5-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Veracode para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26e5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="f26e5-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="f26e5-139">Para establecer la relación de vínculo, en Veracode, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f26e5-140">Para configurar y probar el inicio de sesión único de Azure AD con Veracode, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f26e5-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f26e5-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="f26e5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f26e5-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f26e5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f26e5-143">**[Creación de un usuario de prueba de Veracode](#create-a-veracode-test-user)**: para tener un homólogo de Britta Simon en Veracode que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26e5-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f26e5-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26e5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f26e5-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="f26e5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f26e5-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f26e5-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="f26e5-148">**Para configurar el inicio de sesión único de Azure AD con Veracode, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f26e5-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="f26e5-149">En Azure Portal, en la página de integración de la aplicación **Veracode**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="f26e5-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f26e5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="f26e5-153">En la sección **Dominio y direcciones URL de Veracode**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="f26e5-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="f26e5-155">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f26e5-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="f26e5-157">El objetivo de esta sección es describir cómo habilitar usuarios para que se autentiquen en Veracode con su cuenta de Azure AD a través de la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="f26e5-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="f26e5-158">La aplicación Veracode espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token de SAML** .</span><span class="sxs-lookup"><span data-stu-id="f26e5-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="f26e5-159">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="f26e5-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="f26e5-160">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f26e5-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="f26e5-161">Para agregar las asignaciones de los atributos necesarios, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f26e5-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="f26e5-162">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="f26e5-162">Attribute Name</span></span> | <span data-ttu-id="f26e5-163">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="f26e5-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="f26e5-164">firstname</span><span class="sxs-lookup"><span data-stu-id="f26e5-164">firstname</span></span> |<span data-ttu-id="f26e5-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="f26e5-165">User.givenname</span></span> |
    | <span data-ttu-id="f26e5-166">lastname</span><span class="sxs-lookup"><span data-stu-id="f26e5-166">lastname</span></span> |<span data-ttu-id="f26e5-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="f26e5-167">User.surname</span></span> |
    | <span data-ttu-id="f26e5-168">email</span><span class="sxs-lookup"><span data-stu-id="f26e5-168">email</span></span> |<span data-ttu-id="f26e5-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="f26e5-169">User.mail</span></span> |
    
    <span data-ttu-id="f26e5-170">a.</span><span class="sxs-lookup"><span data-stu-id="f26e5-170">a.</span></span> <span data-ttu-id="f26e5-171">En cada fila de datos de la tabla anterior, haga clic en **agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="f26e5-172">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f26e5-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="f26e5-173">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f26e5-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="f26e5-174">b.</span><span class="sxs-lookup"><span data-stu-id="f26e5-174">b.</span></span> <span data-ttu-id="f26e5-175">En el cuadro de texto **Nombre de atributo** , escriba el nombre de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="f26e5-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f26e5-176">c.</span><span class="sxs-lookup"><span data-stu-id="f26e5-176">c.</span></span> <span data-ttu-id="f26e5-177">En el cuadro de texto **Valor de atributo** , seleccione el valor de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="f26e5-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f26e5-178">d.</span><span class="sxs-lookup"><span data-stu-id="f26e5-178">d.</span></span> <span data-ttu-id="f26e5-179">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-179">Click **Ok**.</span></span>

7. <span data-ttu-id="f26e5-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f26e5-180">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f26e5-182">En la sección **Configuración de Veracode**, haga clic en **Configurar Veracode** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f26e5-183">Copie el **identificador de entidad de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuración de Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="f26e5-185">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Veracode como administrador.</span><span class="sxs-lookup"><span data-stu-id="f26e5-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="f26e5-186">En el menú de la parte superior, haga clic en **Configuración** y luego en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="f26e5-187">![Administración](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f26e5-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="f26e5-188">Haga clic en la pestaña **SAML** .</span><span class="sxs-lookup"><span data-stu-id="f26e5-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="f26e5-189">En la sección **Configuración de SAML de organización** siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f26e5-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f26e5-190">![Administración](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f26e5-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="f26e5-191">a.</span><span class="sxs-lookup"><span data-stu-id="f26e5-191">a.</span></span>  <span data-ttu-id="f26e5-192">En el cuadro de texto **Issuer** (Emisor), pegue el valor de **Identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f26e5-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f26e5-193">b.</span><span class="sxs-lookup"><span data-stu-id="f26e5-193">b.</span></span> <span data-ttu-id="f26e5-194">Para cargar el certificado descargado de Azure Portal, haga clic en **Choose file** (Elegir archivo).</span><span class="sxs-lookup"><span data-stu-id="f26e5-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="f26e5-195">c.</span><span class="sxs-lookup"><span data-stu-id="f26e5-195">c.</span></span> <span data-ttu-id="f26e5-196">Seleccione **Habilitar registro automático**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="f26e5-197">En la sección **Configuración de registro automático**, siga este procedimiento y, después, haga clic en **Guardar**:</span><span class="sxs-lookup"><span data-stu-id="f26e5-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="f26e5-198">![Administración](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f26e5-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="f26e5-199">a.</span><span class="sxs-lookup"><span data-stu-id="f26e5-199">a.</span></span> <span data-ttu-id="f26e5-200">Como **Activación de nuevo usuario**, seleccione **No se requiere ninguna activación**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="f26e5-201">b.</span><span class="sxs-lookup"><span data-stu-id="f26e5-201">b.</span></span> <span data-ttu-id="f26e5-202">Como **Actualizaciones de datos de usuario**, seleccione **Datos de usuario de Veracode de preferencia**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="f26e5-203">c.</span><span class="sxs-lookup"><span data-stu-id="f26e5-203">c.</span></span> <span data-ttu-id="f26e5-204">Para **Detalles de atributo de SAML**, seleccione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f26e5-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="f26e5-205">**Roles de usuario**</span><span class="sxs-lookup"><span data-stu-id="f26e5-205">**User Roles**</span></span>
      * <span data-ttu-id="f26e5-206">**Administrador de directivas**</span><span class="sxs-lookup"><span data-stu-id="f26e5-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="f26e5-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="f26e5-207">**Reviewer**</span></span>
      * <span data-ttu-id="f26e5-208">**Principal de seguridad**</span><span class="sxs-lookup"><span data-stu-id="f26e5-208">**Security Lead**</span></span>
      * <span data-ttu-id="f26e5-209">**Ejecutivo**</span><span class="sxs-lookup"><span data-stu-id="f26e5-209">**Executive**</span></span>
      * <span data-ttu-id="f26e5-210">**Remitente**</span><span class="sxs-lookup"><span data-stu-id="f26e5-210">**Submitter**</span></span>
      * <span data-ttu-id="f26e5-211">**Creador**</span><span class="sxs-lookup"><span data-stu-id="f26e5-211">**Creator**</span></span>
      * <span data-ttu-id="f26e5-212">**Todos los tipos de detección**</span><span class="sxs-lookup"><span data-stu-id="f26e5-212">**All Scan Types**</span></span>
      * <span data-ttu-id="f26e5-213">**Pertenencias a equipos**</span><span class="sxs-lookup"><span data-stu-id="f26e5-213">**Team Memberships**</span></span>
      * <span data-ttu-id="f26e5-214">**Equipo predeterminado**</span><span class="sxs-lookup"><span data-stu-id="f26e5-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="f26e5-215">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f26e5-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f26e5-216">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f26e5-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f26e5-217">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f26e5-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f26e5-218">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-218">Create an Azure AD test user</span></span>

<span data-ttu-id="f26e5-219">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f26e5-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="f26e5-221">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f26e5-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f26e5-222">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f26e5-224">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f26e5-226">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f26e5-228">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f26e5-228">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f26e5-230">a.</span><span class="sxs-lookup"><span data-stu-id="f26e5-230">a.</span></span> <span data-ttu-id="f26e5-231">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f26e5-232">b.</span><span class="sxs-lookup"><span data-stu-id="f26e5-232">b.</span></span> <span data-ttu-id="f26e5-233">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f26e5-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f26e5-234">c.</span><span class="sxs-lookup"><span data-stu-id="f26e5-234">c.</span></span> <span data-ttu-id="f26e5-235">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f26e5-236">d.</span><span class="sxs-lookup"><span data-stu-id="f26e5-236">d.</span></span> <span data-ttu-id="f26e5-237">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="f26e5-238">Creación de un usuario de prueba de Veracode</span><span class="sxs-lookup"><span data-stu-id="f26e5-238">Create a Veracode test user</span></span>
<span data-ttu-id="f26e5-239">Para permitir que los usuarios de Azure AD inicien sesión en Veracode, deben aprovisionarse en Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="f26e5-240">En el caso de Veracode, el aprovisionamiento es una tarea automatizada.</span><span class="sxs-lookup"><span data-stu-id="f26e5-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="f26e5-241">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="f26e5-241">There is no action item for you.</span></span> <span data-ttu-id="f26e5-242">Los usuarios se crean automáticamente si es necesario durante el primer intento de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f26e5-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="f26e5-243">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Veracode ofrecida por Veracode para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26e5-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f26e5-244">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26e5-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="f26e5-245">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="f26e5-247">**Para asignar a Britta Simon a Veracode, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="f26e5-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="f26e5-248">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f26e5-250">En la lista de aplicaciones, seleccione **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-250">In the applications list, select **Veracode**.</span></span>

    ![Vínculo a Veracode en la lista de aplicaciones](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="f26e5-252">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="f26e5-254">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-254">Click **Add** button.</span></span> <span data-ttu-id="f26e5-255">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="f26e5-257">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f26e5-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f26e5-258">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f26e5-259">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f26e5-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f26e5-260">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f26e5-260">Test single sign-on</span></span>

<span data-ttu-id="f26e5-261">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f26e5-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f26e5-262">Al hacer clic en el icono de Veracode en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Veracode.</span><span class="sxs-lookup"><span data-stu-id="f26e5-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="f26e5-263">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f26e5-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f26e5-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f26e5-264">Additional resources</span></span>

* [<span data-ttu-id="f26e5-265">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f26e5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f26e5-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f26e5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

