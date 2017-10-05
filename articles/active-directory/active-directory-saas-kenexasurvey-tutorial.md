---
title: "Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e IBM Kenexa Survey Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="98299-103">Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="98299-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="98299-104">En este tutorial, aprenderá a integrar IBM Kenexa Survey Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98299-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98299-105">La integración de IBM Kenexa Survey Enterprise con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="98299-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98299-106">Puede controlar en Azure AD quién tiene acceso a IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="98299-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="98299-107">Puede permitir que los usuarios inicien sesión automáticamente en IBM Kenexa Survey Enterprise mediante el inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98299-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="98299-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="98299-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="98299-109">Si quiere obtener más información sobre la integración de aplicaciones de software como servicio (SaaS) con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98299-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98299-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98299-110">Prerequisites</span></span>

<span data-ttu-id="98299-111">Para configurar la integración de Azure AD con IBM Kenexa Survey Enterprise, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="98299-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="98299-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98299-113">Una suscripción habilitada para el inicio de sesión único en IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="98299-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98299-114">No se recomienda usar un entorno de producción para probar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="98299-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="98299-115">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="98299-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="98299-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="98299-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98299-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98299-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98299-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="98299-118">Scenario description</span></span>
<span data-ttu-id="98299-119">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="98299-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="98299-120">El escenario descrito en el tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="98299-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="98299-121">Adición de IBM Kenexa Survey Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="98299-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="98299-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="98299-123">Agregar IBM Kenexa Survey Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="98299-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="98299-124">Para configurar la integración de IBM Kenexa Survey Enterprise en Azure AD, agregue IBM Kenexa Survey Enterprise desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="98299-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98299-125">Para agregar IBM Kenexa Survey Enterprise desde la galería, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98299-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="98299-126">En el panel izquierdo de [Azure Portal](https://portal.azure.com), haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98299-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="98299-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98299-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="98299-130">Para agregar una aplicación, haga clic en el botón **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="98299-130">To add an application, click the **New application** button.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="98299-132">En el cuadro de búsqueda, escriba **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="98299-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="98299-134">En la lista de resultados, seleccione **IBM Kenexa Survey Enterprise** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98299-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa Survey Enterprise en la lista de resultados](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="98299-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="98299-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="98299-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98299-138">Para que el inicio de sesión único funcione, Azure AD debe identificar el usuario homólogo de IBM Kenexa Survey Enterprise en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98299-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="98299-139">Es decir, Azure AD debe establecer una relación de vínculo entre un usuario de Azure AD y un usuario relacionado de IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="98299-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="98299-140">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de IBM Kenexa Survey Enterprise como valor de **nombre de usuario** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98299-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="98299-141">Para configurar y probar el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise, complete los bloques de creación de las dos secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="98299-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="98299-142">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="98299-143">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación IBM Kenexa Survey Enterprise siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98299-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="98299-144">En Azure Portal, en la página de integración de la aplicación **IBM Kenexa Survey Enterprise**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="98299-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo de inicio de sesión único de IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="98299-146">En el cuadro de diálogo **Inicio de sesión único**, en el cuadro **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="98299-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="98299-148">En la sección **Dominio y direcciones URL de IBM Kenexa Survey Enterprise**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98299-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="98299-150">a.</span><span class="sxs-lookup"><span data-stu-id="98299-150">a.</span></span> <span data-ttu-id="98299-151">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="98299-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="98299-152">b.</span><span class="sxs-lookup"><span data-stu-id="98299-152">b.</span></span> <span data-ttu-id="98299-153">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="98299-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98299-154">Los valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="98299-154">The preceding values are not real.</span></span> <span data-ttu-id="98299-155">Actualícelos con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="98299-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="98299-156">Para obtener los valores reales, póngase en contacto con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="98299-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="98299-157">En **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98299-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![Vínculo de descarga del certificado (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="98299-159">La aplicación IBM Kenexa Survey Enterprise espera recibir las aserciones del Lenguaje de marcado de aserción de seguridad (SAML) en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos de token de SAML.</span><span class="sxs-lookup"><span data-stu-id="98299-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="98299-160">El valor de la notificación de identificador de usuario en la respuesta debe coincidir con el Id. de inicio de sesión único configurado en el sistema Kenexa.</span><span class="sxs-lookup"><span data-stu-id="98299-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="98299-161">Para asignar el identificador de usuario adecuado en su organización como Protocolo de datagramas de Internet (IDP) de inicio de sesión único, trabaje con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="98299-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="98299-162">De forma predeterminada, Azure AD establece el identificador de usuario como el valor de nombre principal de usuario (UPN).</span><span class="sxs-lookup"><span data-stu-id="98299-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="98299-163">Puede cambiar este valor en la pestaña **Atributo**, como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="98299-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="98299-164">La integración solo funciona después de haber completado correctamente la asignación.</span><span class="sxs-lookup"><span data-stu-id="98299-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![El cuadro de diálogo Atributos de usuario](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="98299-166">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="98299-166">Click **Save**.</span></span>

    ![Botón Guardar de Configurar inicio de sesión único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98299-168">Para abrir la ventana **Configurar inicio de sesión**, en la sección **Configuración de IBM Kenexa Survey Enterprise**, haga clic en **Configurar IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="98299-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![El vínculo Configurar IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="98299-170">Copie los valores de **Sign-Out URL** (Dirección URL de cierre de sesión), **SAML Entity ID** (Identificador de entidad de SAML) y **SAML single sign-on Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="98299-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="98299-171">En la ventana **Configurar inicio de sesión**, bajo **Referencia rápida**, copie los valores de **Sign-Out URL**, **SAML Entity ID** y **SAML single sign-on Service URL**.</span><span class="sxs-lookup"><span data-stu-id="98299-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="98299-172">Para configurar el inicio de sesión único en **IBM Kenexa Survey Enterprise**, envíe los valores descargados de **Certificado (Base64)**, **Sign-Out URL** (Dirección URL de cierre de sesión), **SAMLSAML Entity ID** (Identificador de entidad de SAML) y **SAML single sign-on Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) al [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="98299-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="98299-173">Puede consultar una versión resumida de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98299-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="98299-174">Después de agregar la aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y obtenga acceso a la documentación insertada a través de la sección **Configuración** de la parte final.</span><span class="sxs-lookup"><span data-stu-id="98299-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="98299-175">Para obtener más información sobre la característica de documentación insertada, vea la [documentación insertada de Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="98299-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="98299-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-176">Create an Azure AD test user</span></span>
<span data-ttu-id="98299-177">En esta sección, creará el usuario de prueba Britta Simon en Azure Portal siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98299-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Creación de un usuario de prueba de Azure AD][100]

1. <span data-ttu-id="98299-179">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98299-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98299-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="98299-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98299-183">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="98299-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98299-185">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="98299-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98299-187">a.</span><span class="sxs-lookup"><span data-stu-id="98299-187">a.</span></span> <span data-ttu-id="98299-188">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98299-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98299-189">b.</span><span class="sxs-lookup"><span data-stu-id="98299-189">b.</span></span> <span data-ttu-id="98299-190">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98299-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="98299-191">c.</span><span class="sxs-lookup"><span data-stu-id="98299-191">c.</span></span> <span data-ttu-id="98299-192">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="98299-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="98299-193">d.</span><span class="sxs-lookup"><span data-stu-id="98299-193">d.</span></span> <span data-ttu-id="98299-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98299-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="98299-195">Creación de un usuario de prueba de IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="98299-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="98299-196">En esta sección, creará un usuario llamado Britta Simon en IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="98299-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="98299-197">Para crear usuarios en el sistema IBM Kenexa Survey Enterprise y asignarles el identificador de SSO, puede trabajar con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="98299-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="98299-198">Este valor de identificador de SSO también debe asignarse al valor user identifier (identificador de usuario) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98299-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="98299-199">Puede cambiar esta configuración predeterminada en la pestaña **Atributo**.</span><span class="sxs-lookup"><span data-stu-id="98299-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="98299-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98299-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="98299-201">En esta sección, concederá acceso al usuario Britta Simon a IBM Kenexa Survey Enterprise para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="98299-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="98299-203">Para asignar al usuario Britta Simon a IBM Kenexa Survey Enterprise, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98299-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="98299-204">En Azure Portal, abra la vista **Aplicaciones**, vaya a la vista **Directorio**, seleccione **Aplicaciones empresariales** y después haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98299-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Vínculos "Aplicaciones empresariales" y "Todas las aplicaciones"][201] 

2. <span data-ttu-id="98299-206">En la lista **Aplicaciones**, seleccione **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="98299-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Vínculo IBM Kenexa Survey Enterprise en la lista Aplicaciones](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="98299-208">En el panel izquierdo, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98299-208">In the left pane, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="98299-210">Haga clic en el botón **Agregar** y, después, en el panel **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98299-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="98299-212">En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="98299-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="98299-213">En el cuadro de diálogo **Usuarios y grupos**, haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="98299-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="98299-214">En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="98299-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="98299-215">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="98299-215">Test single sign-on</span></span>

<span data-ttu-id="98299-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="98299-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="98299-217">Al hacer clic en el icono de **IBM Kenexa Survey Enterprise** en el panel de acceso, debería iniciar sesión automáticamente en su aplicación IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="98299-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98299-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="98299-218">Additional resources</span></span>

* [<span data-ttu-id="98299-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98299-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98299-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98299-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
