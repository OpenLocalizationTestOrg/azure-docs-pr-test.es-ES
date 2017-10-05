---
title: "Tutorial: Integración de Azure Active Directory con Work.com | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="919b7-103">Tutorial: Integración de Azure Active Directory con Work.com</span><span class="sxs-lookup"><span data-stu-id="919b7-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="919b7-104">En este tutorial, obtendrá información sobre cómo integrar Work.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="919b7-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="919b7-105">La integración de Work.com con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="919b7-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="919b7-106">Puede controlar en Azure AD quién tiene acceso a Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="919b7-107">Puede permitir que los usuarios inicien sesión automáticamente en Work.com (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b7-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="919b7-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="919b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="919b7-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="919b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="919b7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="919b7-110">Prerequisites</span></span>

<span data-ttu-id="919b7-111">Para configurar la integración de Azure AD con Work.com, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="919b7-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="919b7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="919b7-113">Una suscripción habilitada para el inicio de sesión único en Work.com</span><span class="sxs-lookup"><span data-stu-id="919b7-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="919b7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="919b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="919b7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="919b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="919b7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="919b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="919b7-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="919b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="919b7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="919b7-118">Scenario description</span></span>
<span data-ttu-id="919b7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="919b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="919b7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="919b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="919b7-121">Agregar Work.com desde la galería</span><span class="sxs-lookup"><span data-stu-id="919b7-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="919b7-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="919b7-123">Agregar Work.com desde la galería</span><span class="sxs-lookup"><span data-stu-id="919b7-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="919b7-124">Para configurar la integración de Work.com en Azure AD, será preciso que agregue Work.com desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="919b7-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="919b7-125">**Para agregar Work.com desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="919b7-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="919b7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="919b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="919b7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="919b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="919b7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="919b7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="919b7-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="919b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="919b7-133">En el cuadro de búsqueda, escriba **Work.com**, seleccione **Work.com** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="919b7-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Incorporación de la aplicación desde la galería](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="919b7-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="919b7-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Work.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="919b7-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="919b7-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Work.com para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="919b7-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="919b7-139">Para establecer la relación de vínculo, en Work.com, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="919b7-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="919b7-140">Para configurar y probar el inicio de sesión único de Azure AD con Work.com, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="919b7-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="919b7-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="919b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="919b7-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="919b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="919b7-143">**[Creación de un usuario de prueba de Work.com](#create-a-workcom-test-user)**: para tener un homólogo de Britta Simon en Work.com que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b7-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="919b7-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="919b7-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="919b7-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="919b7-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="919b7-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="919b7-148">Para configurar el inicio de sesión único, deberá configurar todavía un nombre de dominio personalizado de Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="919b7-149">Deberá definir al menos un nombre de dominio, probar su nombre de dominio e implementarlo en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="919b7-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="919b7-150">**Para configurar el inicio de sesión único de Azure AD con Work.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="919b7-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="919b7-151">En Azure Portal, en la página de integración de la aplicación **Work.com**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="919b7-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="919b7-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="919b7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="919b7-155">En la sección **Dominio y direcciones URL de Work.com**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="919b7-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Sección Dominio y direcciones URL de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="919b7-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `http://<companyname>.my.salesforce.com`.</span><span class="sxs-lookup"><span data-stu-id="919b7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="919b7-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="919b7-158">This value is not real.</span></span> <span data-ttu-id="919b7-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="919b7-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="919b7-160">Póngase en contacto con el [equipo de soporte al cliente de Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="919b7-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="919b7-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="919b7-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="919b7-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="919b7-163">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="919b7-165">En la sección **Configuración de Work.com**, haga clic en **Configurar Work.com** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="919b7-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="919b7-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="919b7-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sección de configuración de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="919b7-168">Inicie sesión en su inquilino de Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="919b7-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="919b7-169">Acceda a **Setup**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="919b7-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="919b7-170">![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="919b7-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="919b7-171">En el panel de navegación izquierdo, en la sección **Administer** (Administrar), haga clic en **Domain Management** (Administración de dominios) para expandir la sección relacionada y, luego, haga clic en **My Domain** (Mi dominio) para abrir la página **My Domain** (Mi dominio).</span><span class="sxs-lookup"><span data-stu-id="919b7-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="919b7-172">![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="919b7-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="919b7-173">Para comprobar que el dominio se configuró correctamente, asegúrese de que está en "**Step 4 Deployed to Users**" (Paso 4 Dominio implementado para usuarios) y revise la sección "**My Domain Settings**" (Mi configuración de dominio).</span><span class="sxs-lookup"><span data-stu-id="919b7-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="919b7-174">![Dominio implementado al usuario](./media/active-directory-saas-work-com-tutorial/ic784377.png "Dominio implementado al usuario")</span><span class="sxs-lookup"><span data-stu-id="919b7-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="919b7-175">Inicie sesión en su inquilino de Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="919b7-176">Acceda a **Setup**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="919b7-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="919b7-177">![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="919b7-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="919b7-178">Expanda el menú **Security Controls** (Controles de seguridad) y luego haga clic en **Single Sign-On Settings** (Configuración de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="919b7-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="919b7-179">![Configuración de inicio de sesión único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="919b7-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="919b7-180">En la página del cuadro de diálogo **Single Sign-On Settings** (Configuración de inicio de sesión único), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="919b7-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="919b7-181">![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")</span><span class="sxs-lookup"><span data-stu-id="919b7-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="919b7-182">a.</span><span class="sxs-lookup"><span data-stu-id="919b7-182">a.</span></span> <span data-ttu-id="919b7-183">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="919b7-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="919b7-184">b.</span><span class="sxs-lookup"><span data-stu-id="919b7-184">b.</span></span> <span data-ttu-id="919b7-185">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="919b7-185">Click **New**.</span></span>

15. <span data-ttu-id="919b7-186">En la sección **SAML Single Sign-On Settings** (Configuración del inicio de sesión único de SAML), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="919b7-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="919b7-187">![Inicio de sesión único SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="919b7-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="919b7-188">a.</span><span class="sxs-lookup"><span data-stu-id="919b7-188">a.</span></span> <span data-ttu-id="919b7-189">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración.</span><span class="sxs-lookup"><span data-stu-id="919b7-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="919b7-190">Si se proporciona un valor para **Name** (Nombre), el cuadro de texto **API Name** (Nombre de API) se completa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="919b7-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="919b7-191">b.</span><span class="sxs-lookup"><span data-stu-id="919b7-191">b.</span></span> <span data-ttu-id="919b7-192">En el cuadro de texto **Emisor**, pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="919b7-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="919b7-193">c.</span><span class="sxs-lookup"><span data-stu-id="919b7-193">c.</span></span> <span data-ttu-id="919b7-194">Para cargar el certificado descargado de Azure Portal, haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="919b7-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="919b7-195">d.</span><span class="sxs-lookup"><span data-stu-id="919b7-195">d.</span></span> <span data-ttu-id="919b7-196">En el cuadro de texto **Id. de identidad**, escriba `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="919b7-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="919b7-197">e.</span><span class="sxs-lookup"><span data-stu-id="919b7-197">e.</span></span> <span data-ttu-id="919b7-198">Como **SAML Identity Type** (Tipo de identidad SAML), seleccione **Assertion contains the Federation ID from the User object** (La aserción contiene el id. de federación del objeto Usuario).</span><span class="sxs-lookup"><span data-stu-id="919b7-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="919b7-199">f.</span><span class="sxs-lookup"><span data-stu-id="919b7-199">f.</span></span> <span data-ttu-id="919b7-200">Para **///SAML Identity Location** (Ubicación de identidad SAML), seleccione **///Identity is in the NameIdentfier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción Subject).</span><span class="sxs-lookup"><span data-stu-id="919b7-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="919b7-201">g.</span><span class="sxs-lookup"><span data-stu-id="919b7-201">g.</span></span> <span data-ttu-id="919b7-202">En el cuadro de texto **Identity Provider Login URL** (Dirección URL de inicio de sesión del proveedor de identidades), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="919b7-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="919b7-203">h.</span><span class="sxs-lookup"><span data-stu-id="919b7-203">h.</span></span> <span data-ttu-id="919b7-204">En el cuadro de texto **Identity Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades), pegue el valor de **dirección URL de cierre de sesión**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="919b7-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="919b7-205">i.</span><span class="sxs-lookup"><span data-stu-id="919b7-205">i.</span></span> <span data-ttu-id="919b7-206">Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP Post** (Método HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="919b7-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="919b7-207">j.</span><span class="sxs-lookup"><span data-stu-id="919b7-207">j.</span></span> <span data-ttu-id="919b7-208">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="919b7-208">Click **Save**.</span></span>

16. <span data-ttu-id="919b7-209">En el portal de Work.com, en el panel de navegación izquierdo, haga clic en **Domain Management** (Administración de dominios) para expandir la sección relacionada y luego haga clic en la página **My Domain** (Mi dominio) para abrir la página **My Domain** (Mi dominio).</span><span class="sxs-lookup"><span data-stu-id="919b7-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="919b7-210">![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="919b7-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="919b7-211">En la página **My domain** (Mi dominio), en la sección **Login Page Branding** (Personalización de marca de la página de inicio de sesión), haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="919b7-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="919b7-212">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="919b7-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="919b7-213">En la página **Login Page Branding** (Personalización de marca de la página de inicio de sesión), en la sección **Authentication Service** (Servicio de autenticación), se muestra el nombre de su **SAML SSO Settings** (Configuración de SSO de SAML).</span><span class="sxs-lookup"><span data-stu-id="919b7-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="919b7-214">Selecciónelo y luego haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="919b7-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="919b7-215">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="919b7-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="919b7-216">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="919b7-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="919b7-217">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="919b7-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="919b7-218">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="919b7-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="919b7-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-219">Create an Azure AD test user</span></span>
<span data-ttu-id="919b7-220">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="919b7-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="919b7-222">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="919b7-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="919b7-223">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="919b7-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="919b7-225">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="919b7-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="919b7-227">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="919b7-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Sumar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="919b7-229">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="919b7-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="919b7-231">a.</span><span class="sxs-lookup"><span data-stu-id="919b7-231">a.</span></span> <span data-ttu-id="919b7-232">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="919b7-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="919b7-233">b.</span><span class="sxs-lookup"><span data-stu-id="919b7-233">b.</span></span> <span data-ttu-id="919b7-234">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="919b7-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="919b7-235">c.</span><span class="sxs-lookup"><span data-stu-id="919b7-235">c.</span></span> <span data-ttu-id="919b7-236">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="919b7-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="919b7-237">d.</span><span class="sxs-lookup"><span data-stu-id="919b7-237">d.</span></span> <span data-ttu-id="919b7-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="919b7-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="919b7-239">Creación de un usuario de prueba de Work.com</span><span class="sxs-lookup"><span data-stu-id="919b7-239">Create a Work.com test user</span></span>
<span data-ttu-id="919b7-240">Para que los usuarios de Azure Active Directory puedan iniciar sesión, deben aprovisionarse a Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="919b7-241">En el caso de Work.com, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="919b7-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="919b7-242">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="919b7-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="919b7-243">Inicie sesión en su sitio de la compañía de Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="919b7-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="919b7-244">Acceda a **Setup**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="919b7-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="919b7-245">![Instalación](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="919b7-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="919b7-246">Vaya a **Manage Users \> (Administrar usuarios) Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="919b7-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="919b7-247">![Administración de usuarios](./media/active-directory-saas-work-com-tutorial/IC784369.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="919b7-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="919b7-248">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="919b7-248">Click **New User**.</span></span>
   
    <span data-ttu-id="919b7-249">![Todos los usuarios](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos los usuarios")</span><span class="sxs-lookup"><span data-stu-id="919b7-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="919b7-250">En la sección Edición de usuarios, realice los pasos siguientes, en los atributos de una cuenta de Azure AD válida que desee aprovisionar en los cuadros de texto relacionados:</span><span class="sxs-lookup"><span data-stu-id="919b7-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="919b7-251">![Edición de usuarios](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edición de usuarios")</span><span class="sxs-lookup"><span data-stu-id="919b7-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="919b7-252">a.</span><span class="sxs-lookup"><span data-stu-id="919b7-252">a.</span></span> <span data-ttu-id="919b7-253">En el cuadro de texto **Nombre**, escriba el **nombre** del usuario **Britta**.</span><span class="sxs-lookup"><span data-stu-id="919b7-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="919b7-254">b.</span><span class="sxs-lookup"><span data-stu-id="919b7-254">b.</span></span> <span data-ttu-id="919b7-255">En el cuadro de texto **Apellido**, escriba el **apellido** del usuario **Simon**.</span><span class="sxs-lookup"><span data-stu-id="919b7-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="919b7-256">c.</span><span class="sxs-lookup"><span data-stu-id="919b7-256">c.</span></span> <span data-ttu-id="919b7-257">En el cuadro de texto **Alias**, escriba el **nombre** del usuario **Britta**.</span><span class="sxs-lookup"><span data-stu-id="919b7-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="919b7-258">d.</span><span class="sxs-lookup"><span data-stu-id="919b7-258">d.</span></span> <span data-ttu-id="919b7-259">En el cuadro de texto **Correo electrónico**, escriba la **dirección de correo electrónico** del usuario, **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="919b7-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="919b7-260">e.</span><span class="sxs-lookup"><span data-stu-id="919b7-260">e.</span></span> <span data-ttu-id="919b7-261">En el cuadro de texto **Nombre de usuario**, escriba un nombre de usuario como **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="919b7-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="919b7-262">f.</span><span class="sxs-lookup"><span data-stu-id="919b7-262">f.</span></span> <span data-ttu-id="919b7-263">En el cuadro de texto **Sobrenombre**, escriba un **sobrenombre** del usuario, como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="919b7-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="919b7-264">g.</span><span class="sxs-lookup"><span data-stu-id="919b7-264">g.</span></span> <span data-ttu-id="919b7-265">Seleccione **Role** (Rol), **User License** (Licencia de usuario) y **Profile** (Perfil).</span><span class="sxs-lookup"><span data-stu-id="919b7-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="919b7-266">h.</span><span class="sxs-lookup"><span data-stu-id="919b7-266">h.</span></span> <span data-ttu-id="919b7-267">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="919b7-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="919b7-268">El titular de la cuenta de Azure AD recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="919b7-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="919b7-269">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="919b7-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="919b7-270">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="919b7-272">**Para asignar el usuario Britta Simon a Work.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="919b7-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="919b7-273">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="919b7-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="919b7-275">En la lista de aplicaciones, seleccione **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="919b7-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com en la lista de la aplicación](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="919b7-277">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="919b7-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="919b7-279">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="919b7-279">Click **Add** button.</span></span> <span data-ttu-id="919b7-280">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="919b7-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="919b7-282">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="919b7-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="919b7-283">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="919b7-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="919b7-284">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="919b7-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="919b7-285">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="919b7-285">Test single sign-on</span></span>

<span data-ttu-id="919b7-286">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="919b7-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="919b7-287">Al hacer clic en el icono de Work.com en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Work.com.</span><span class="sxs-lookup"><span data-stu-id="919b7-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="919b7-288">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="919b7-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="919b7-289">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="919b7-289">Additional resources</span></span>

* [<span data-ttu-id="919b7-290">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="919b7-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="919b7-291">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="919b7-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

