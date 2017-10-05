---
title: "Tutorial: Integración de Azure Active Directory con Onit | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="3360f-103">Tutorial: Integración de Azure Active Directory con Onit</span><span class="sxs-lookup"><span data-stu-id="3360f-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="3360f-104">En este tutorial, obtendrá información sobre cómo integrar Onit con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3360f-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3360f-105">La integración de Onit con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3360f-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3360f-106">Puede controlar en Azure AD quién tiene acceso a Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="3360f-107">Puede permitir que los usuarios inicien sesión automáticamente en Onit (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3360f-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3360f-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3360f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3360f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3360f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3360f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3360f-110">Prerequisites</span></span>

<span data-ttu-id="3360f-111">Para configurar la integración de Azure AD con Onit se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3360f-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="3360f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3360f-113">Una suscripción habilitada para el inicio de sesión único en Onit</span><span class="sxs-lookup"><span data-stu-id="3360f-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3360f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3360f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3360f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3360f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3360f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3360f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3360f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3360f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3360f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3360f-118">Scenario description</span></span>

<span data-ttu-id="3360f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3360f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3360f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3360f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3360f-121">Agregación de Onit desde la galería</span><span class="sxs-lookup"><span data-stu-id="3360f-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="3360f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="3360f-123">Agregación de Onit desde la galería</span><span class="sxs-lookup"><span data-stu-id="3360f-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="3360f-124">Para configurar la integración de Onit en Azure AD, deberá agregar Onit desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3360f-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3360f-125">**Para agregar Onit desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3360f-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3360f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3360f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="3360f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3360f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3360f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3360f-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="3360f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3360f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="3360f-133">En el cuadro de búsqueda, escriba **Onit**, seleccione **Onit** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3360f-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![Onit en la lista de resultados](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3360f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3360f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Onit con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3360f-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3360f-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Onit para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3360f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="3360f-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="3360f-139">Para establecer la relación de vínculo, en Onit, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3360f-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3360f-140">Para configurar y probar el inicio de sesión único de Azure AD con Onit, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3360f-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3360f-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="3360f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3360f-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3360f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3360f-143">**[Creación de un usuario de prueba de Onit](#create-an-onit-test-user)** : para tener un homólogo de Britta Simon en Onit que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3360f-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3360f-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3360f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3360f-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**, para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3360f-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3360f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3360f-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="3360f-148">**Para configurar el inicio de sesión único de Azure AD con Onit, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3360f-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="3360f-149">En Azure Portal, en la página de integración de la aplicación **Onit**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3360f-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="3360f-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3360f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="3360f-153">En la sección **Dominio y direcciones URL de Onit**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3360f-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="3360f-155">a.</span><span class="sxs-lookup"><span data-stu-id="3360f-155">a.</span></span> <span data-ttu-id="3360f-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<sub-domain>.onit.com`.</span><span class="sxs-lookup"><span data-stu-id="3360f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="3360f-157">b.</span><span class="sxs-lookup"><span data-stu-id="3360f-157">b.</span></span> <span data-ttu-id="3360f-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="3360f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3360f-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3360f-159">These values are not real.</span></span> <span data-ttu-id="3360f-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3360f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3360f-161">Póngase en contacto con el [equipo de soporte técnico de Onit](https://www.onit.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3360f-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="3360f-162">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="3360f-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="3360f-164">La aplicación Onit espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="3360f-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3360f-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="3360f-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="3360f-166">Puede administrar el valor de estos atributos desde la pestaña **"Atributo"** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3360f-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="3360f-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="3360f-167">The following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="3360f-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3360f-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3360f-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="3360f-170">Attribute Name</span></span> | <span data-ttu-id="3360f-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="3360f-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="3360f-172">email</span><span class="sxs-lookup"><span data-stu-id="3360f-172">email</span></span> | <span data-ttu-id="3360f-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="3360f-173">user.mail</span></span> |
    
    <span data-ttu-id="3360f-174">a.</span><span class="sxs-lookup"><span data-stu-id="3360f-174">a.</span></span> <span data-ttu-id="3360f-175">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="3360f-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3360f-178">b.</span><span class="sxs-lookup"><span data-stu-id="3360f-178">b.</span></span> <span data-ttu-id="3360f-179">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="3360f-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3360f-180">c.</span><span class="sxs-lookup"><span data-stu-id="3360f-180">c.</span></span> <span data-ttu-id="3360f-181">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="3360f-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3360f-182">d.</span><span class="sxs-lookup"><span data-stu-id="3360f-182">d.</span></span> <span data-ttu-id="3360f-183">Deje **Espacio de nombres** en blanco.</span><span class="sxs-lookup"><span data-stu-id="3360f-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="3360f-184">e.</span><span class="sxs-lookup"><span data-stu-id="3360f-184">e.</span></span> <span data-ttu-id="3360f-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3360f-185">Click **Ok**.</span></span>

7. <span data-ttu-id="3360f-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3360f-186">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3360f-188">En la sección **Configuración de Onit**, haga clic en **Configurar Onit** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3360f-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3360f-189">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3360f-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="3360f-191">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de Onit de la compañía.</span><span class="sxs-lookup"><span data-stu-id="3360f-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="3360f-192">En el menú de la parte superior, haga clic en **Administration**(Administración).</span><span class="sxs-lookup"><span data-stu-id="3360f-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="3360f-193">![Administración](./media/active-directory-saas-onit-tutorial/IC791174.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="3360f-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="3360f-194">Haga clic en **Edit Corporation**(Editar corporación).</span><span class="sxs-lookup"><span data-stu-id="3360f-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="3360f-195">![Editar corporación](./media/active-directory-saas-onit-tutorial/IC791175.png "Editar corporación")</span><span class="sxs-lookup"><span data-stu-id="3360f-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="3360f-196">Haga clic en la pestaña **Security** (Seguridad).</span><span class="sxs-lookup"><span data-stu-id="3360f-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="3360f-197">![Editar información de la compañía](./media/active-directory-saas-onit-tutorial/IC791176.png "Editar información de la compañía")</span><span class="sxs-lookup"><span data-stu-id="3360f-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="3360f-198">En la pestaña **Seguridad** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3360f-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="3360f-199">![Inicio de sesión único](./media/active-directory-saas-onit-tutorial/IC791177.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="3360f-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="3360f-200">a.</span><span class="sxs-lookup"><span data-stu-id="3360f-200">a.</span></span> <span data-ttu-id="3360f-201">Como **Estrategia de autenticación**, seleccione **Inicio de sesión único y contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3360f-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="3360f-202">b.</span><span class="sxs-lookup"><span data-stu-id="3360f-202">b.</span></span> <span data-ttu-id="3360f-203">En el cuadro de texto **Idp Target URL** (Dirección URL de destino del Idp), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3360f-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3360f-204">c.</span><span class="sxs-lookup"><span data-stu-id="3360f-204">c.</span></span> <span data-ttu-id="3360f-205">En el cuadro de texto **IDP Logout URL** (Dirección URL de cierre de sesión del IDP), pegue el valor de la **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3360f-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3360f-206">d.</span><span class="sxs-lookup"><span data-stu-id="3360f-206">d.</span></span> <span data-ttu-id="3360f-207">En el cuadro de texto **Idp Cert Fingerprint (SHA1)** (Huella digital de certificado del Idp [SHA1]), pegue el valor de **Huella digital** del certificado que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3360f-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="3360f-208">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3360f-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3360f-209">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3360f-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3360f-210">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3360f-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3360f-211">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-211">Create an Azure AD test user</span></span>

<span data-ttu-id="3360f-212">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3360f-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="3360f-214">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3360f-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3360f-215">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3360f-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3360f-217">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3360f-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3360f-219">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3360f-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3360f-221">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3360f-221">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3360f-223">a.</span><span class="sxs-lookup"><span data-stu-id="3360f-223">a.</span></span> <span data-ttu-id="3360f-224">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3360f-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3360f-225">b.</span><span class="sxs-lookup"><span data-stu-id="3360f-225">b.</span></span> <span data-ttu-id="3360f-226">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3360f-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3360f-227">c.</span><span class="sxs-lookup"><span data-stu-id="3360f-227">c.</span></span> <span data-ttu-id="3360f-228">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3360f-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3360f-229">d.</span><span class="sxs-lookup"><span data-stu-id="3360f-229">d.</span></span> <span data-ttu-id="3360f-230">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3360f-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="3360f-231">Creación de un usuario de prueba de Onit</span><span class="sxs-lookup"><span data-stu-id="3360f-231">Create an Onit test user</span></span>

<span data-ttu-id="3360f-232">Para permitir que los usuarios de Azure AD inicien sesión en Onit, tienen que aprovisionarse en Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="3360f-233">En el caso de Onit, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3360f-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="3360f-234">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="3360f-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3360f-235">Inicie sesión en su sitio de la compañía de **Onit** como administrador.</span><span class="sxs-lookup"><span data-stu-id="3360f-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="3360f-236">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3360f-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="3360f-237">![Administración](./media/active-directory-saas-onit-tutorial/IC791180.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="3360f-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="3360f-238">En la página del cuadro de diálogo **Add User** (Agregar usuario), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3360f-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="3360f-239">![Agregar usuario](./media/active-directory-saas-onit-tutorial/IC791181.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="3360f-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="3360f-240">Escriba el **Nombre** y la **Dirección de correo electrónico** de una cuenta de Azure AD válida que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="3360f-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="3360f-241">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3360f-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="3360f-242">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="3360f-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3360f-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3360f-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="3360f-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="3360f-246">**Para asignar al usuario Britta Simon a Onit, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3360f-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="3360f-247">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3360f-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3360f-249">En la lista de aplicaciones, seleccione **Onit**.</span><span class="sxs-lookup"><span data-stu-id="3360f-249">In the applications list, select **Onit**.</span></span>

    ![Vínculo a Onit en la lista de aplicaciones](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="3360f-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3360f-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="3360f-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3360f-253">Click **Add** button.</span></span> <span data-ttu-id="3360f-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3360f-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="3360f-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3360f-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3360f-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3360f-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3360f-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3360f-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3360f-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3360f-259">Test single sign-on</span></span>

<span data-ttu-id="3360f-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3360f-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3360f-261">Al hacer clic en el icono de Onit en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Onit.</span><span class="sxs-lookup"><span data-stu-id="3360f-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="3360f-262">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3360f-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3360f-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3360f-263">Additional resources</span></span>

* [<span data-ttu-id="3360f-264">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3360f-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3360f-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3360f-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

