---
title: "Tutorial: Integración de Azure Active Directory con TimeOffManager | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="54e7a-103">Tutorial: Integración de Azure Active Directory con TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="54e7a-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="54e7a-104">En este tutorial, obtendrá información sobre cómo integrar TimeOffManager con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54e7a-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54e7a-105">La integración de TimeOffManager con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="54e7a-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54e7a-106">Puede controlar en Azure AD quién tiene acceso a TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="54e7a-107">Puede habilitar que los usuarios inicien sesión automáticamente en TimeOffManager (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54e7a-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54e7a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="54e7a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54e7a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54e7a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54e7a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="54e7a-110">Prerequisites</span></span>

<span data-ttu-id="54e7a-111">Para configurar la integración de Azure AD con TimeOffManager, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="54e7a-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="54e7a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54e7a-113">Una suscripción habilitada para inicio de sesión único en TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="54e7a-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54e7a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="54e7a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54e7a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="54e7a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54e7a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="54e7a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54e7a-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54e7a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54e7a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="54e7a-118">Scenario description</span></span>
<span data-ttu-id="54e7a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="54e7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54e7a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="54e7a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54e7a-121">Adición de TimeOffManager desde la galería</span><span class="sxs-lookup"><span data-stu-id="54e7a-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="54e7a-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="54e7a-123">Adición de TimeOffManager desde la galería</span><span class="sxs-lookup"><span data-stu-id="54e7a-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="54e7a-124">Para configurar la integración de TimeOffManager en Azure AD, deberá agregar TimeOffManager desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="54e7a-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54e7a-125">**Para agregar TimeOffManager desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="54e7a-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54e7a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54e7a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54e7a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="54e7a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54e7a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="54e7a-133">En el cuadro de búsqueda, escriba **TimeOffManager**, seleccione **TimeOffManager** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54e7a-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Incorporación desde la galería](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="54e7a-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="54e7a-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TimeOffManager utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54e7a-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54e7a-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TimeOffManager para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54e7a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="54e7a-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="54e7a-139">Para establecer la relación de vínculo, en TimeOffManager, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54e7a-140">Para configurar y probar el inicio de sesión único de Azure AD con TimeOffManager, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="54e7a-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54e7a-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="54e7a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54e7a-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54e7a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54e7a-143">**[Creación de un usuario de prueba de TimeOffManager](#create-a-timeoffmanager-test-user)**: para tener un homólogo de Britta Simon en TimeOffManager que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54e7a-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54e7a-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54e7a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54e7a-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="54e7a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54e7a-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="54e7a-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="54e7a-148">**Para configurar el inicio de sesión único de Azure AD con TimeOffManager, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="54e7a-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="54e7a-149">En Azure Portal, en la página de integración de la aplicación **TimeOffManager**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="54e7a-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="54e7a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="54e7a-153">En la sección **Dominio y direcciones URL de TimeOffManager**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="54e7a-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![Sección Dominio y direcciones URL de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="54e7a-155">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`.</span><span class="sxs-lookup"><span data-stu-id="54e7a-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54e7a-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="54e7a-156">This value is not real.</span></span> <span data-ttu-id="54e7a-157">Actualice este valor con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="54e7a-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="54e7a-158">Puede obtener este valor en la **página de configuración de Inicio de sesión único** que se explica más adelante en el tutorial o ponerse en contacto con el [equipo de soporte técnico de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="54e7a-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="54e7a-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="54e7a-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="54e7a-161">El objetivo de esta sección es describir cómo se habilita la autenticación de usuarios en TimeOffManager con su cuenta de Azure AD mediante la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="54e7a-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="54e7a-162">La aplicación TimeOffManager espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token SAML.</span><span class="sxs-lookup"><span data-stu-id="54e7a-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="54e7a-163">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="54e7a-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="54e7a-164">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="54e7a-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="54e7a-165">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="54e7a-165">Attribute Name</span></span> | <span data-ttu-id="54e7a-166">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="54e7a-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="54e7a-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="54e7a-167">Firstname</span></span> |<span data-ttu-id="54e7a-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="54e7a-168">User.givenname</span></span> |
    | <span data-ttu-id="54e7a-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="54e7a-169">Lastname</span></span> |<span data-ttu-id="54e7a-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="54e7a-170">User.surname</span></span> |
    | <span data-ttu-id="54e7a-171">Email</span><span class="sxs-lookup"><span data-stu-id="54e7a-171">Email</span></span> |<span data-ttu-id="54e7a-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="54e7a-172">User.mail</span></span> |
    
    <span data-ttu-id="54e7a-173">a.</span><span class="sxs-lookup"><span data-stu-id="54e7a-173">a.</span></span>  <span data-ttu-id="54e7a-174">En cada fila de datos de la tabla anterior, haga clic en **agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="54e7a-175">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="54e7a-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="54e7a-176">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="54e7a-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="54e7a-177">b.</span><span class="sxs-lookup"><span data-stu-id="54e7a-177">b.</span></span>  <span data-ttu-id="54e7a-178">En el cuadro de texto **Nombre de atributo** , escriba el nombre de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="54e7a-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="54e7a-179">c.</span><span class="sxs-lookup"><span data-stu-id="54e7a-179">c.</span></span>  <span data-ttu-id="54e7a-180">En el cuadro de texto **Valor de atributo** , seleccione el valor de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="54e7a-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="54e7a-181">d.</span><span class="sxs-lookup"><span data-stu-id="54e7a-181">d.</span></span>  <span data-ttu-id="54e7a-182">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="54e7a-183">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="54e7a-183">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="54e7a-185">En la sección **Configuración de TimeOffManager**, haga clic en **Configurar TimeOffManager** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54e7a-186">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sección Configuración de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="54e7a-188">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="54e7a-189">Vaya a **Cuenta \> Opciones de cuenta \> Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="54e7a-190">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="54e7a-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="54e7a-191">En la sección **Configuración del inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="54e7a-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="54e7a-192">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="54e7a-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="54e7a-193">a.</span><span class="sxs-lookup"><span data-stu-id="54e7a-193">a.</span></span> <span data-ttu-id="54e7a-194">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego pegue todo el certificado en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="54e7a-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="54e7a-195">b.</span><span class="sxs-lookup"><span data-stu-id="54e7a-195">b.</span></span> <span data-ttu-id="54e7a-196">En el cuadro de texto **Emisor de IdP**, pegue el valor de **Identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="54e7a-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="54e7a-197">c.</span><span class="sxs-lookup"><span data-stu-id="54e7a-197">c.</span></span> <span data-ttu-id="54e7a-198">En el cuadro de texto **Dirección URL del punto de conexión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="54e7a-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="54e7a-199">d.</span><span class="sxs-lookup"><span data-stu-id="54e7a-199">d.</span></span> <span data-ttu-id="54e7a-200">En **Aplicar SAML**, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="54e7a-201">e.</span><span class="sxs-lookup"><span data-stu-id="54e7a-201">e.</span></span> <span data-ttu-id="54e7a-202">En **Crear usuarios automáticamente**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="54e7a-203">f.</span><span class="sxs-lookup"><span data-stu-id="54e7a-203">f.</span></span> <span data-ttu-id="54e7a-204">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="54e7a-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="54e7a-205">g.</span><span class="sxs-lookup"><span data-stu-id="54e7a-205">g.</span></span> <span data-ttu-id="54e7a-206">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="54e7a-207">En la página **Configuración de inicio de sesión único**, copie el valor de **URL del Servicio de consumidor de aserciones** y péguelo en el cuadro de texto **URL de respuesta** bajo la sección **Dominio y direcciones URL de TimeOffManager** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="54e7a-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="54e7a-208">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="54e7a-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="54e7a-209">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54e7a-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54e7a-210">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="54e7a-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54e7a-211">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54e7a-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54e7a-212">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-212">Create an Azure AD test user</span></span>
<span data-ttu-id="54e7a-213">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54e7a-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="54e7a-215">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="54e7a-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54e7a-216">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54e7a-218">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos --> Todos los usuarios](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54e7a-220">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54e7a-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54e7a-222">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="54e7a-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54e7a-224">a.</span><span class="sxs-lookup"><span data-stu-id="54e7a-224">a.</span></span> <span data-ttu-id="54e7a-225">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54e7a-226">b.</span><span class="sxs-lookup"><span data-stu-id="54e7a-226">b.</span></span> <span data-ttu-id="54e7a-227">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54e7a-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54e7a-228">c.</span><span class="sxs-lookup"><span data-stu-id="54e7a-228">c.</span></span> <span data-ttu-id="54e7a-229">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54e7a-230">d.</span><span class="sxs-lookup"><span data-stu-id="54e7a-230">d.</span></span> <span data-ttu-id="54e7a-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="54e7a-232">Creación de un usuario de prueba de TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="54e7a-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="54e7a-233">Para permitir que los usuarios de Azure AD inicien sesión en TimeOffManager, deben aprovisionarse en TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="54e7a-234">TimeOffManager admite aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="54e7a-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="54e7a-235">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="54e7a-235">There is no action item for you.</span></span>  

<span data-ttu-id="54e7a-236">Los usuarios se agregan automáticamente durante el primer inicio de sesión mediante el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="54e7a-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="54e7a-237">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TimeOffManager ofrecida por TimeOffManager para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54e7a-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54e7a-238">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="54e7a-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="54e7a-239">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="54e7a-241">**Para asignar a Britta Simon a TimeOffManager, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="54e7a-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="54e7a-242">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="54e7a-244">En la lista de aplicaciones, seleccione **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-244">In the applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager en la lista de aplicaciones](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="54e7a-246">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="54e7a-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-248">Click **Add** button.</span></span> <span data-ttu-id="54e7a-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="54e7a-251">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="54e7a-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54e7a-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54e7a-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="54e7a-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="54e7a-254">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="54e7a-254">Test single sign-on</span></span>

<span data-ttu-id="54e7a-255">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="54e7a-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54e7a-256">Al hacer clic en el icono de TimeOffManager en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="54e7a-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="54e7a-257">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54e7a-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54e7a-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="54e7a-258">Additional resources</span></span>

* [<span data-ttu-id="54e7a-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54e7a-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54e7a-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54e7a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

