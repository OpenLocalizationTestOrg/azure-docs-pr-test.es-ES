---
title: "Tutorial: Integración de Azure Active Directory con PolicyStat | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="85b50-103">Tutorial: Integración de Azure Active Directory con PolicyStat</span><span class="sxs-lookup"><span data-stu-id="85b50-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="85b50-104">En este tutorial, aprenderá a integrar PolicyStat con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85b50-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85b50-105">La integración de PolicyStat con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="85b50-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85b50-106">Puede controlar en Azure AD quién tiene acceso a PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="85b50-107">Puede permitir que los usuarios inicien sesión automáticamente en PolicyStat (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b50-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85b50-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="85b50-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="85b50-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85b50-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85b50-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85b50-110">Prerequisites</span></span>

<span data-ttu-id="85b50-111">Para configurar la integración de Azure AD con PolicyStat, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="85b50-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="85b50-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85b50-113">Una suscripción habilitada para el inicio de sesión único en PolicyStat</span><span class="sxs-lookup"><span data-stu-id="85b50-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85b50-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="85b50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85b50-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="85b50-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85b50-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="85b50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85b50-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85b50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85b50-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="85b50-118">Scenario description</span></span>
<span data-ttu-id="85b50-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="85b50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85b50-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="85b50-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85b50-121">Incorporación de PolicyStat desde la galería</span><span class="sxs-lookup"><span data-stu-id="85b50-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="85b50-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="85b50-123">Incorporación de PolicyStat desde la galería</span><span class="sxs-lookup"><span data-stu-id="85b50-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="85b50-124">Para configurar la integración de PolicyStat en Azure AD, es preciso agregar PolicyStat desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="85b50-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85b50-125">**Para agregar PolicyStat desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="85b50-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85b50-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85b50-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85b50-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="85b50-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85b50-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="85b50-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="85b50-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="85b50-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="85b50-133">En el cuadro de búsqueda, escriba **PolicySta**.</span><span class="sxs-lookup"><span data-stu-id="85b50-133">In the search box, type **PolicyStat**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="85b50-135">En el panel de resultados, seleccione **PolicyStat** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85b50-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85b50-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85b50-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con PolicyStat con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85b50-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85b50-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de PolicyStat para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b50-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="85b50-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="85b50-141">Para establecer la relación de vínculo en PolicyStat, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="85b50-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="85b50-142">Para configurar y probar el inicio de sesión único de Azure AD con PolicyStat, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="85b50-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85b50-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="85b50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85b50-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85b50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85b50-145">**[Creación de un usuario de prueba de PolicyStat](#creating-a-policystat-test-user)**: para tener un homólogo de Britta Simon en PolicyStat vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b50-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85b50-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b50-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85b50-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="85b50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85b50-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85b50-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="85b50-150">**Para configurar el inicio de sesión único de Azure AD con PolicyStat, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="85b50-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="85b50-151">En Azure Portal, en la página de integración de la aplicación **PolicyStat**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="85b50-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="85b50-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="85b50-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="85b50-155">En la sección **Dominio y direcciones URL de PolicyStat**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85b50-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="85b50-157">a.</span><span class="sxs-lookup"><span data-stu-id="85b50-157">a.</span></span> <span data-ttu-id="85b50-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.policystat.com`.</span><span class="sxs-lookup"><span data-stu-id="85b50-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="85b50-159">b.</span><span class="sxs-lookup"><span data-stu-id="85b50-159">b.</span></span> <span data-ttu-id="85b50-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="85b50-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85b50-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="85b50-161">These values are not real.</span></span> <span data-ttu-id="85b50-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="85b50-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85b50-163">Póngase en contacto con el [equipo de soporte al cliente de PolicyStat](http://www.policystat.com/support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="85b50-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="85b50-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="85b50-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="85b50-166">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en PolicyStat con su cuenta de Azure AD usando el protocolo SAML basado en la federación.</span><span class="sxs-lookup"><span data-stu-id="85b50-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="85b50-167">La aplicación PolicyStat espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token de SAML**.</span><span class="sxs-lookup"><span data-stu-id="85b50-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="85b50-168">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="85b50-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="85b50-169">![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="85b50-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="85b50-170">Para agregar las asignaciones de los atributos necesarios, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85b50-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="85b50-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="85b50-171">Attribute Name</span></span>    |   <span data-ttu-id="85b50-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="85b50-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="85b50-173">uid</span><span class="sxs-lookup"><span data-stu-id="85b50-173">uid</span></span> | <span data-ttu-id="85b50-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="85b50-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="85b50-175">a.</span><span class="sxs-lookup"><span data-stu-id="85b50-175">a.</span></span> <span data-ttu-id="85b50-176">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="85b50-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="85b50-179">b.</span><span class="sxs-lookup"><span data-stu-id="85b50-179">b.</span></span> <span data-ttu-id="85b50-180">En el cuadro de texto **Nombre de atributo**, escriba **uid**.</span><span class="sxs-lookup"><span data-stu-id="85b50-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="85b50-181">c.</span><span class="sxs-lookup"><span data-stu-id="85b50-181">c.</span></span> <span data-ttu-id="85b50-182">En el cuadro de texto **Valor del atributo**, seleccione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="85b50-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="85b50-183">d.</span><span class="sxs-lookup"><span data-stu-id="85b50-183">d.</span></span> <span data-ttu-id="85b50-184">En la lista **Correo**, seleccione **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="85b50-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="85b50-185">e.</span><span class="sxs-lookup"><span data-stu-id="85b50-185">e.</span></span> <span data-ttu-id="85b50-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="85b50-186">Click **Ok**</span></span>

7. <span data-ttu-id="85b50-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="85b50-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="85b50-189">En otra ventana del explorador web, inicie sesión en el sitio de la compañía PolicyStat como administrador.</span><span class="sxs-lookup"><span data-stu-id="85b50-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="85b50-190">Haga clic en la pestaña **Administración** y en **Configuración de inicio de sesión único** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="85b50-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="85b50-191">![Menú Administrator](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menú Administrator")</span><span class="sxs-lookup"><span data-stu-id="85b50-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="85b50-192">En la sección **Configuración**, seleccione **Habilitar la integración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="85b50-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="85b50-193">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="85b50-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="85b50-194">Haga clic en **Configurar atributos** y, en la sección **Configurar atributos**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85b50-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="85b50-195">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="85b50-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="85b50-196">a.</span><span class="sxs-lookup"><span data-stu-id="85b50-196">a.</span></span> <span data-ttu-id="85b50-197">En el cuadro de texto **Atributo de nombre de usuario**, escriba **uid**.</span><span class="sxs-lookup"><span data-stu-id="85b50-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="85b50-198">b.</span><span class="sxs-lookup"><span data-stu-id="85b50-198">b.</span></span> <span data-ttu-id="85b50-199">En el cuadro de texto **Atributo de nombre**, escriba el **nombre** del usuario, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="85b50-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="85b50-200">c.</span><span class="sxs-lookup"><span data-stu-id="85b50-200">c.</span></span> <span data-ttu-id="85b50-201">En el cuadro de texto **Atributo de apellido**, escriba el **apellido** del usuario, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="85b50-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="85b50-202">d.</span><span class="sxs-lookup"><span data-stu-id="85b50-202">d.</span></span> <span data-ttu-id="85b50-203">En el cuadro de texto **Atributo de correo electrónico**, escriba la **dirección de correo electrónico** del usuario, **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="85b50-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="85b50-204">e.</span><span class="sxs-lookup"><span data-stu-id="85b50-204">e.</span></span> <span data-ttu-id="85b50-205">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="85b50-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="85b50-206">Haga clic en **Sus metadatos de IDP** y en la sección **Sus metadatos de IDP**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="85b50-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="85b50-207">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="85b50-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="85b50-208">a.</span><span class="sxs-lookup"><span data-stu-id="85b50-208">a.</span></span> <span data-ttu-id="85b50-209">Abra el archivo de metadatos descargado, copie el contenido y luego péguelo en el cuadro de texto **Metadatos del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="85b50-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="85b50-210">b.</span><span class="sxs-lookup"><span data-stu-id="85b50-210">b.</span></span> <span data-ttu-id="85b50-211">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="85b50-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="85b50-212">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85b50-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="85b50-213">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="85b50-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="85b50-214">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85b50-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85b50-215">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="85b50-216">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85b50-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="85b50-218">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="85b50-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85b50-219">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85b50-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85b50-221">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="85b50-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85b50-223">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="85b50-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85b50-225">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="85b50-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85b50-227">a.</span><span class="sxs-lookup"><span data-stu-id="85b50-227">a.</span></span> <span data-ttu-id="85b50-228">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85b50-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85b50-229">b.</span><span class="sxs-lookup"><span data-stu-id="85b50-229">b.</span></span> <span data-ttu-id="85b50-230">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85b50-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85b50-231">c.</span><span class="sxs-lookup"><span data-stu-id="85b50-231">c.</span></span> <span data-ttu-id="85b50-232">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="85b50-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="85b50-233">d.</span><span class="sxs-lookup"><span data-stu-id="85b50-233">d.</span></span> <span data-ttu-id="85b50-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="85b50-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="85b50-235">Creación de un usuario de prueba de PolicyStat</span><span class="sxs-lookup"><span data-stu-id="85b50-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="85b50-236">Para permitir que los usuarios de Azure AD inicien sesión en PolicyStat, deben aprovisionarse en PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="85b50-237">PolicyStat admite aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="85b50-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="85b50-238">Esto significa que no es necesario agregar usuarios manualmente a PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="85b50-239">Los usuarios se agregarán automáticamente en su primer inicio de sesión a través del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="85b50-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="85b50-240">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de PolicyStat ofrecida por PolicyStat para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b50-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="85b50-241">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b50-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="85b50-242">En esta sección, concederá acceso a Britta Simon a PolicyStat para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="85b50-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="85b50-244">**Para asignar a Britta Simon a PolicyStat, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="85b50-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="85b50-245">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="85b50-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="85b50-247">En la lista de aplicaciones, seleccione **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="85b50-247">In the applications list, select **PolicyStat**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="85b50-249">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="85b50-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="85b50-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="85b50-251">Click **Add** button.</span></span> <span data-ttu-id="85b50-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="85b50-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="85b50-254">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="85b50-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85b50-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="85b50-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85b50-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="85b50-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85b50-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="85b50-257">Testing single sign-on</span></span>

<span data-ttu-id="85b50-258">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="85b50-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85b50-259">Al hacer clic en el icono de PolicyStat en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="85b50-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="85b50-260">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85b50-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85b50-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="85b50-261">Additional resources</span></span>

* [<span data-ttu-id="85b50-262">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85b50-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85b50-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85b50-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

