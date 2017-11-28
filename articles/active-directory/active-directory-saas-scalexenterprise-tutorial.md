---
title: "Tutorial: Integración de Azure Active Directory con ScaleX Enterprise | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="59853-103">Tutorial: Integración de Azure Active Directory con ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="59853-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="59853-104">En este tutorial, aprenderá a integrar ScaleX Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59853-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59853-105">La integración de ScaleX Enterprise con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="59853-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59853-106">Puede controlar en Azure AD quién tiene acceso a ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="59853-107">Puede permitir que los usuarios inicien sesión automáticamente en ScaleX Enterprise (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59853-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59853-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="59853-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59853-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="59853-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="59853-110">¿Qué es el acceso a aplicaciones y el inicio de sesión único con [Azure Active Directory](active-directory-appssoaccess-whatis.md)?</span><span class="sxs-lookup"><span data-stu-id="59853-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59853-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="59853-111">Prerequisites</span></span>

<span data-ttu-id="59853-112">Para configurar la integración de Azure AD con ScaleX Enterprise, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="59853-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="59853-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-113">An Azure AD subscription</span></span>
- <span data-ttu-id="59853-114">Una suscripción habilitada para el inicio de sesión único en ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="59853-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59853-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="59853-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59853-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="59853-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59853-117">No use su entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="59853-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="59853-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59853-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59853-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="59853-119">Scenario description</span></span>
<span data-ttu-id="59853-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="59853-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59853-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="59853-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59853-122">Adición de ScaleX Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="59853-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="59853-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="59853-124">Adición de ScaleX Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="59853-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="59853-125">Para configurar la integración de ScaleX Enterprise en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="59853-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59853-126">**Para agregar ScaleX Enterprise desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="59853-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59853-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59853-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59853-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="59853-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59853-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59853-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="59853-132">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="59853-132">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="59853-134">En el cuadro de búsqueda, escriba **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="59853-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="59853-136">En el panel de resultados, seleccione **ScaleX Enterprise** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59853-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59853-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59853-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ScaleX Enterprise utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59853-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59853-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ScaleX Enterprise para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59853-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="59853-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="59853-142">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="59853-143">Para configurar y probar el inicio de sesión único de Azure AD con ScaleX Enterprise, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="59853-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59853-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="59853-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59853-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59853-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59853-146">**[Creación de un usuario de prueba de ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**: para tener un homólogo de Britta Simon en ScaleX Enterprise que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59853-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59853-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59853-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59853-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="59853-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59853-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59853-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="59853-151">**Para configurar el inicio de sesión único de Azure AD con ScaleX Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="59853-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="59853-152">En Azure Portal, en la página de integración de la aplicación **ScaleX Enterprise**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="59853-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="59853-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="59853-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="59853-156">En la sección **Dominio y direcciones URL de ScaleX Enterprise**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="59853-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="59853-158">a.</span><span class="sxs-lookup"><span data-stu-id="59853-158">a.</span></span> <span data-ttu-id="59853-159">En el cuadro de texto **Identificador**, escriba el valor con el siguiente patrón: `https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="59853-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="59853-160">b.</span><span class="sxs-lookup"><span data-stu-id="59853-160">b.</span></span> <span data-ttu-id="59853-161">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://platform.rescale.com/saml2/<company id>/acs/`.</span><span class="sxs-lookup"><span data-stu-id="59853-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="59853-162">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="59853-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="59853-164">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="59853-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="59853-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="59853-165">These are not the real values.</span></span> <span data-ttu-id="59853-166">Actualice estos valores con los valores reales de Identificador, URL de respuesta o URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="59853-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="59853-167">Póngase en contacto con el [equipo de soporte de cliente de ScaleX Enterprise](http://info.rescale.com/contact_sales) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="59853-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="59853-168">La aplicación ScaleX Enterprise espera las aserciones de SAML en un formato específico, que requiere que se modifiquen las asignaciones de atributos personalizados en la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="59853-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="59853-169">Haga clic en **Ver y editar todos los demás atributos de usuario** para abrir la configuración de atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="59853-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="59853-171">a.</span><span class="sxs-lookup"><span data-stu-id="59853-171">a.</span></span> <span data-ttu-id="59853-172">Haga clic con el botón derecho en el **nombre** del atributo y luego haga clic en Eliminar.</span><span class="sxs-lookup"><span data-stu-id="59853-172">Right click the attribute **name** and click delete.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="59853-174">b.</span><span class="sxs-lookup"><span data-stu-id="59853-174">b.</span></span> <span data-ttu-id="59853-175">Haga clic en el atributo **emailaddress** para abrir la ventana Editar atributo.</span><span class="sxs-lookup"><span data-stu-id="59853-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="59853-176">Cambie el valor de **user.mail** a **user.userprincipalname** y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="59853-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="59853-178">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="59853-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="59853-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="59853-180">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="59853-182">En la sección **Configuración de ScaleX Enterprise**, haga clic en **Configurar ScaleX Enterprise** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="59853-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="59853-183">Copie **SAML Entity ID** y **SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="59853-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="59853-185">Para configurar el inicio de sesión único en **ScaleX Enterprise**, regístrese en el sitio web de la compañía de ScaleX Enterprise como administrador.</span><span class="sxs-lookup"><span data-stu-id="59853-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="59853-186">Haga clic en el menú en la esquina superior derecha y seleccione **Contoso Administration** (Administración de Contoso).</span><span class="sxs-lookup"><span data-stu-id="59853-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59853-187">Contoso solo es un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="59853-187">Contoso is just an example.</span></span> <span data-ttu-id="59853-188">Debería tratarse del nombre real de la empresa.</span><span class="sxs-lookup"><span data-stu-id="59853-188">This should be your actual Company Name.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="59853-190">Seleccione **Integrations** (Integraciones) en el menú superior y seleccione **Single Sign-On** (Inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="59853-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="59853-192">Complete el formulario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="59853-192">Complete the form as follows:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="59853-194">a.</span><span class="sxs-lookup"><span data-stu-id="59853-194">a.</span></span> <span data-ttu-id="59853-195">Seleccione **"Create any user who can authenticate with SSO"** (Crear cualquier usuario que se pueda autenticar con SSO).</span><span class="sxs-lookup"><span data-stu-id="59853-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="59853-196">b.</span><span class="sxs-lookup"><span data-stu-id="59853-196">b.</span></span> <span data-ttu-id="59853-197">**Service Provider saml** (SAML del proveedor de servicios): pegue el valor ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***.</span><span class="sxs-lookup"><span data-stu-id="59853-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="59853-198">c.</span><span class="sxs-lookup"><span data-stu-id="59853-198">c.</span></span> <span data-ttu-id="59853-199">**Name of Identity Provider email field in ACS response** (Nombre de campo de correo electrónico del proveedor de identidades en respuestas de ACS): pegue el valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="59853-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="59853-200">d.</span><span class="sxs-lookup"><span data-stu-id="59853-200">d.</span></span> <span data-ttu-id="59853-201">**Identity Provider EntityDescriptor Entity ID** (Id. de entidad EntityDescriptor del proveedor de identidades): pegue el valor del **identificador de entidad en SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="59853-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="59853-202">e.</span><span class="sxs-lookup"><span data-stu-id="59853-202">e.</span></span> <span data-ttu-id="59853-203">**Identity Provider SingleSignOnService URL** (Dirección URL del servicio de inicio de sesión único del proveedor de identidades): pegue la **dirección URL del servicio de inicio de sesión único de SAML** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="59853-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="59853-204">f.</span><span class="sxs-lookup"><span data-stu-id="59853-204">f.</span></span> <span data-ttu-id="59853-205">**Identity Provider public X509 certificate** (Certificado X509 público del proveedor de identidades): abra el certificado X509 descargado de Azure Portal en el Bloc de notas y pegue el contenido en este cuadro.</span><span class="sxs-lookup"><span data-stu-id="59853-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="59853-206">Asegúrese de que no haya saltos de línea en el medio del contenido del certificado.</span><span class="sxs-lookup"><span data-stu-id="59853-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="59853-207">g.</span><span class="sxs-lookup"><span data-stu-id="59853-207">g.</span></span> <span data-ttu-id="59853-208">Active las casillas siguientes: **Enabled, Encrypt NameID y Sign AuthnRequests.** (Habilitado, Cifrar Id. de nombre y Firmar solicitudes de autenticación).</span><span class="sxs-lookup"><span data-stu-id="59853-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="59853-209">h.</span><span class="sxs-lookup"><span data-stu-id="59853-209">h.</span></span> <span data-ttu-id="59853-210">Haga clic en **Update SSO Settings** (Actualizar configuración de SSO) para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="59853-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="59853-211">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59853-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59853-212">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="59853-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59853-213">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59853-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59853-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="59853-215">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59853-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="59853-217">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="59853-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59853-218">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59853-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59853-220">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="59853-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59853-222">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="59853-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59853-224">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="59853-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59853-226">a.</span><span class="sxs-lookup"><span data-stu-id="59853-226">a.</span></span> <span data-ttu-id="59853-227">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59853-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59853-228">b.</span><span class="sxs-lookup"><span data-stu-id="59853-228">b.</span></span> <span data-ttu-id="59853-229">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59853-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59853-230">c.</span><span class="sxs-lookup"><span data-stu-id="59853-230">c.</span></span> <span data-ttu-id="59853-231">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="59853-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59853-232">d.</span><span class="sxs-lookup"><span data-stu-id="59853-232">d.</span></span> <span data-ttu-id="59853-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="59853-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="59853-234">Creación de un usuario de prueba de ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="59853-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="59853-235">Para permitir que los usuarios de Azure AD se registren en ScaleX Enterprise, deben aprovisionarse en ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="59853-236">En el caso de ScaleX Enterprise, el aprovisionamiento es una tarea automática y no se requiere ningún paso manual.</span><span class="sxs-lookup"><span data-stu-id="59853-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="59853-237">Todos los usuarios que se pueden autenticar correctamente con las credenciales de SSO se aprovisionarán automáticamente en ScaleX.</span><span class="sxs-lookup"><span data-stu-id="59853-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59853-238">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59853-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="59853-239">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="59853-241">**Para asignar el usuario Britta Simon a ScaleX Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="59853-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="59853-242">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59853-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="59853-244">En la lista de aplicaciones, seleccione **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="59853-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="59853-246">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="59853-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="59853-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59853-248">Click **Add** button.</span></span> <span data-ttu-id="59853-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="59853-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="59853-251">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="59853-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59853-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="59853-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59853-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="59853-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="59853-254">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="59853-254">Testing single sign-on</span></span>

<span data-ttu-id="59853-255">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="59853-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59853-256">Al hacer clic en el icono de ScaleX Enterprise del panel de acceso, iniciará sesión automáticamente en la aplicación ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59853-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="59853-257">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="59853-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="59853-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="59853-258">Additional resources</span></span>

* [<span data-ttu-id="59853-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59853-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59853-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59853-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

