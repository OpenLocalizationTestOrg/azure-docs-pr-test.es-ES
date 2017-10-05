---
title: "Tutorial: integración de Azure Active Directory con CloudPassage | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="9d73f-103">Tutorial: integración de Azure Active Directory con CloudPassage</span><span class="sxs-lookup"><span data-stu-id="9d73f-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="9d73f-104">En este tutorial, aprenderá a integrar CloudPassage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d73f-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d73f-105">La integración de CloudPassage con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9d73f-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d73f-106">Puede controlar en Azure AD quién tiene acceso a CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="9d73f-107">Puede permitir que los usuarios inicien sesión automáticamente en CloudPassage (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d73f-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d73f-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9d73f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d73f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d73f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d73f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d73f-110">Prerequisites</span></span>

<span data-ttu-id="9d73f-111">Para configurar la integración de Azure AD con CloudPassage, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9d73f-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="9d73f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d73f-113">Una suscripción habilitada para el inicio de sesión único en CloudPassage</span><span class="sxs-lookup"><span data-stu-id="9d73f-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d73f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9d73f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d73f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9d73f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d73f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9d73f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d73f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d73f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d73f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9d73f-118">Scenario description</span></span>
<span data-ttu-id="9d73f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d73f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d73f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9d73f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d73f-121">Adición de CloudPassage desde la galería</span><span class="sxs-lookup"><span data-stu-id="9d73f-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="9d73f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="9d73f-123">Adición de CloudPassage desde la galería</span><span class="sxs-lookup"><span data-stu-id="9d73f-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="9d73f-124">Para configurar la integración de CloudPassage en Azure AD, deberá agregar CloudPassage desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9d73f-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d73f-125">**Para agregar CloudPassage desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9d73f-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d73f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d73f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d73f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9d73f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d73f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9d73f-133">En el cuadro de búsqueda, escriba **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-133">In the search box, type **CloudPassage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="9d73f-135">En el panel de resultados, seleccione **CloudPassage** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d73f-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d73f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d73f-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con CloudPassage con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d73f-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d73f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de CloudPassage para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d73f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="9d73f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="9d73f-141">Para establecer la relación de vínculo, en CloudPassage, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d73f-142">Para configurar y probar el inicio de sesión único de Azure AD con CloudPassage, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9d73f-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d73f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9d73f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d73f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d73f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d73f-145">**[Creación de un usuario de prueba de CloudPassage](#creating-a-cloudpassage-test-user)**: para tener un homólogo de Britta Simon en CloudPassage que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d73f-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d73f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d73f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d73f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9d73f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d73f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d73f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="9d73f-150">**Para configurar el inicio de sesión único de Azure AD con CloudPassage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9d73f-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="9d73f-151">En Azure Portal, en la página de integración de la aplicación **CloudPassage**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9d73f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d73f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="9d73f-155">En la sección **Dominio y direcciones URL de CloudPassage**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9d73f-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="9d73f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d73f-157">a.</span></span> <span data-ttu-id="9d73f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://portal.cloudpassage.com/saml/init/accountid`.</span><span class="sxs-lookup"><span data-stu-id="9d73f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="9d73f-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d73f-159">b.</span></span> <span data-ttu-id="9d73f-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="9d73f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="9d73f-161">Para obtener el valor de este atributo, haga clic en **SSO Setup documentation** (Documentación de instalación de inicio de sesión única) en la sección **Single Sign-on Settings** (Configuración de inicio de sesión único) del portal de CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="9d73f-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9d73f-163">These values are not real.</span></span> <span data-ttu-id="9d73f-164">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9d73f-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9d73f-165">Póngase en contacto con el [equipo de soporte de cliente de CloudPassage](https://www.cloudpassage.com/company/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9d73f-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="9d73f-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9d73f-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="9d73f-168">La aplicación CloudPassage espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="9d73f-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="9d73f-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="9d73f-169">The following screenshot shows an example for this.</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="9d73f-171">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9d73f-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="9d73f-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="9d73f-172">Attribute Name</span></span> | <span data-ttu-id="9d73f-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="9d73f-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9d73f-174">firstname</span><span class="sxs-lookup"><span data-stu-id="9d73f-174">firstname</span></span> |<span data-ttu-id="9d73f-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9d73f-175">user.givenname</span></span> |
    | <span data-ttu-id="9d73f-176">lastname</span><span class="sxs-lookup"><span data-stu-id="9d73f-176">lastname</span></span> |<span data-ttu-id="9d73f-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="9d73f-177">user.surname</span></span> |
    | <span data-ttu-id="9d73f-178">email</span><span class="sxs-lookup"><span data-stu-id="9d73f-178">email</span></span> |<span data-ttu-id="9d73f-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="9d73f-179">user.mail</span></span> |
    
    <span data-ttu-id="9d73f-180">a.</span><span class="sxs-lookup"><span data-stu-id="9d73f-180">a.</span></span> <span data-ttu-id="9d73f-181">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="9d73f-184">b.</span><span class="sxs-lookup"><span data-stu-id="9d73f-184">b.</span></span> <span data-ttu-id="9d73f-185">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="9d73f-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9d73f-186">c.</span><span class="sxs-lookup"><span data-stu-id="9d73f-186">c.</span></span> <span data-ttu-id="9d73f-187">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="9d73f-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9d73f-188">d.</span><span class="sxs-lookup"><span data-stu-id="9d73f-188">d.</span></span> <span data-ttu-id="9d73f-189">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-189">Click **Ok**.</span></span>

7. <span data-ttu-id="9d73f-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9d73f-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="9d73f-192">En la sección **Configuración de CloudPassage**, haga clic en **Configurar CloudPassage** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d73f-193">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="9d73f-195">En otra ventana del explorador, inicie sesión en su sitio de la compañía de CloudPassage como administrador.</span><span class="sxs-lookup"><span data-stu-id="9d73f-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="9d73f-196">En el menú de la parte superior, haga clic en **Settings** (Configuración) y en **Site Administration** (Administración del sitio).</span><span class="sxs-lookup"><span data-stu-id="9d73f-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configurar inicio de sesión único][12]

11. <span data-ttu-id="9d73f-198">Haga clic en la pestaña **Authentication Settings** (Configuración de autenticación).</span><span class="sxs-lookup"><span data-stu-id="9d73f-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configurar inicio de sesión único][13]

12. <span data-ttu-id="9d73f-200">En la sección **Single Sign-on Settings** (Configuración del inicio de sesión único), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9d73f-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configurar inicio de sesión único][14]

    <span data-ttu-id="9d73f-202">a.</span><span class="sxs-lookup"><span data-stu-id="9d73f-202">a.</span></span> <span data-ttu-id="9d73f-203">Seleccione la casilla **Enable Single sign-on(SSO)(SSO Setup Documentation)** (Habilitar el inicio de sesión único (SSO) (Documentación de configuración de SSO)).</span><span class="sxs-lookup"><span data-stu-id="9d73f-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="9d73f-204">b.</span><span class="sxs-lookup"><span data-stu-id="9d73f-204">b.</span></span> <span data-ttu-id="9d73f-205">Pegue el **identificador de entidad de SAML** en el cuadro de texto **URL del emisor de SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="9d73f-206">c.</span><span class="sxs-lookup"><span data-stu-id="9d73f-206">c.</span></span> <span data-ttu-id="9d73f-207">Pegue **Dirección URL del servicio de inicio de sesión único de SAML** en el cuadro de texto **Dirección URL del punto de conexión de SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="9d73f-208">d.</span><span class="sxs-lookup"><span data-stu-id="9d73f-208">d.</span></span> <span data-ttu-id="9d73f-209">Pegue **Dirección URL de cierre de sesión** en el cuadro de texto **Logout landing page** (Página de aterrizaje de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="9d73f-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="9d73f-210">e.</span><span class="sxs-lookup"><span data-stu-id="9d73f-210">e.</span></span> <span data-ttu-id="9d73f-211">Abra el certificado descargado en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **Certificado x 509**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="9d73f-212">f.</span><span class="sxs-lookup"><span data-stu-id="9d73f-212">f.</span></span> <span data-ttu-id="9d73f-213">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9d73f-214">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d73f-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d73f-215">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9d73f-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d73f-216">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d73f-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d73f-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d73f-218">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d73f-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9d73f-220">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9d73f-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d73f-221">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d73f-223">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d73f-225">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d73f-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d73f-227">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9d73f-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d73f-229">a.</span><span class="sxs-lookup"><span data-stu-id="9d73f-229">a.</span></span> <span data-ttu-id="9d73f-230">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d73f-231">b.</span><span class="sxs-lookup"><span data-stu-id="9d73f-231">b.</span></span> <span data-ttu-id="9d73f-232">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d73f-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d73f-233">c.</span><span class="sxs-lookup"><span data-stu-id="9d73f-233">c.</span></span> <span data-ttu-id="9d73f-234">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d73f-235">d.</span><span class="sxs-lookup"><span data-stu-id="9d73f-235">d.</span></span> <span data-ttu-id="9d73f-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="9d73f-237">Creación de un usuario de prueba de CloudPassage</span><span class="sxs-lookup"><span data-stu-id="9d73f-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="9d73f-238">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="9d73f-239">**Para crear un usuario llamado Britta Simon en CloudPassage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9d73f-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="9d73f-240">Inicie sesión en su sitio de la compañía de **CloudPassage** como administrador.</span><span class="sxs-lookup"><span data-stu-id="9d73f-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="9d73f-241">En la barra de herramientas de la parte superior, haga clic en **Settings** (Configuración) y en **Site Administration** (Administración del sitio).</span><span class="sxs-lookup"><span data-stu-id="9d73f-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Creación de un usuario de prueba de CloudPassage][22] 

3. <span data-ttu-id="9d73f-243">Haga clic en la pestaña **Users** (Usuarios) y, a continuación, en **Add New User** (Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="9d73f-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Creación de un usuario de prueba de CloudPassage][23]

4. <span data-ttu-id="9d73f-245">En la sección **Agregar nuevo usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9d73f-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Creación de un usuario de prueba de CloudPassage][24]
    
    <span data-ttu-id="9d73f-247">a.</span><span class="sxs-lookup"><span data-stu-id="9d73f-247">a.</span></span> <span data-ttu-id="9d73f-248">En el cuadro de texto **First Name** (Nombre), escriba Britta.</span><span class="sxs-lookup"><span data-stu-id="9d73f-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="9d73f-249">b.</span><span class="sxs-lookup"><span data-stu-id="9d73f-249">b.</span></span> <span data-ttu-id="9d73f-250">En el cuadro de texto **Last Name** (Apellidos), escriba Simon.</span><span class="sxs-lookup"><span data-stu-id="9d73f-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="9d73f-251">c.</span><span class="sxs-lookup"><span data-stu-id="9d73f-251">c.</span></span> <span data-ttu-id="9d73f-252">En el cuadro de texto **Username** (Nombre de usuario), el cuadro de texto **Email** (Correo electrónico) y el cuadro de texto **Retype Email** (Volver a escribir correo electrónico), escriba el nombre de usuario de Britta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d73f-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="9d73f-253">d.</span><span class="sxs-lookup"><span data-stu-id="9d73f-253">d.</span></span> <span data-ttu-id="9d73f-254">En **Access Type** (Tipo de acceso), seleccione **Enable Halo Portal Access** (Habilitar el acceso de Portal de Halo).</span><span class="sxs-lookup"><span data-stu-id="9d73f-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="9d73f-255">e.</span><span class="sxs-lookup"><span data-stu-id="9d73f-255">e.</span></span> <span data-ttu-id="9d73f-256">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d73f-257">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d73f-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d73f-258">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9d73f-260">**Para asignar un usuario llamado Britta Simon a CloudPassage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9d73f-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="9d73f-261">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9d73f-263">En la lista de aplicaciones, seleccione **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-263">In the applications list, select **CloudPassage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="9d73f-265">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9d73f-267">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-267">Click **Add** button.</span></span> <span data-ttu-id="9d73f-268">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9d73f-270">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9d73f-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d73f-271">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d73f-272">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d73f-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d73f-273">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9d73f-273">Testing single sign-on</span></span>

<span data-ttu-id="9d73f-274">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9d73f-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9d73f-275">Al hacer clic en el icono de CloudPassage en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="9d73f-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d73f-276">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9d73f-276">Additional resources</span></span>

* [<span data-ttu-id="9d73f-277">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d73f-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d73f-278">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d73f-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

