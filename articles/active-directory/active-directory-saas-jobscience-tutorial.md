---
title: "Tutorial: Integración de Azure Active Directory con Jobscience | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="e4c8b-103">Tutorial: Integración de Azure Active Directory con Jobscience</span><span class="sxs-lookup"><span data-stu-id="e4c8b-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="e4c8b-104">En este tutorial, aprenderá a integrar Jobscience con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4c8b-105">La integración de Jobscience con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4c8b-106">En Azure AD puede controlar quién tiene acceso a Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="e4c8b-107">Puede permitir que los usuarios inicien sesión automáticamente en Jobscience (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4c8b-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e4c8b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4c8b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e4c8b-110">Prerequisites</span></span>

<span data-ttu-id="e4c8b-111">Para configurar la integración de Azure AD con Jobscience, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="e4c8b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4c8b-113">Una suscripción habilitada para inicio de sesión único en Jobscience</span><span class="sxs-lookup"><span data-stu-id="e4c8b-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4c8b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4c8b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4c8b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4c8b-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4c8b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e4c8b-118">Scenario description</span></span>
<span data-ttu-id="e4c8b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4c8b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4c8b-121">Incorporación de Jobscience desde la galería</span><span class="sxs-lookup"><span data-stu-id="e4c8b-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="e4c8b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="e4c8b-123">Incorporación de Jobscience desde la galería</span><span class="sxs-lookup"><span data-stu-id="e4c8b-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="e4c8b-124">Para configurar la integración de Jobscience en Azure AD, deberá agregar Jobscience desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4c8b-125">**Para agregar Jobscience desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e4c8b-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4c8b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4c8b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4c8b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e4c8b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e4c8b-133">En el cuadro de búsqueda, escriba **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-133">In the search box, type **Jobscience**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="e4c8b-135">En el panel de resultados, seleccione **Jobscience** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4c8b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4c8b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jobscience con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e4c8b-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e4c8b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Jobscience para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="e4c8b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="e4c8b-141">Para establecer la relación de vínculo, en Jobscience, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e4c8b-142">Para configurar y probar el inicio de sesión único de Azure AD con Jobscience, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4c8b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e4c8b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4c8b-145">**[Creación de un usuario de prueba de Jobscience](#creating-a-jobscience-test-user)**: para tener un homólogo de Britta Simon en Jobscience que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4c8b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4c8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4c8b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4c8b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="e4c8b-150">**Para configurar el inicio de sesión único de Azure AD con Jobscience, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e4c8b-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="e4c8b-151">En Azure Portal, en la página de integración de la aplicación **Jobscience**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e4c8b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="e4c8b-155">En la sección **Dominio y direcciones URL de Jobscience**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="e4c8b-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e4c8b-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e4c8b-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-158">This value is not real.</span></span> <span data-ttu-id="e4c8b-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e4c8b-160">Puede obtener este valor con el [equipo de soporte técnico del cliente de Jobscience](https://www.jobscience.com/support) o en el perfil de SSO que va a crear, lo que se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="e4c8b-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="e4c8b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e4c8b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4c8b-165">En la sección **Configuración de Jobscience**, haga clic en **Configurar Jobscience** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e4c8b-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="e4c8b-168">Inicie sesión como administrador en el sitio de la compañía de Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="e4c8b-169">Acceda a **Setup**(Configuración).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="e4c8b-170">![Instalación](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="e4c8b-171">En el panel de navegación izquierdo, en la sección **Administer** (Administrar), haga clic en **Domain Management** (Administración de dominios) para expandir la sección relacionada y, luego, haga clic en **My Domain** (Mi dominio) para abrir la página **My Domain** (Mi dominio).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="e4c8b-172">![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="e4c8b-173">Para comprobar que el dominio se configuró correctamente, asegúrese de que está en "**Step 4 Deployed to Users**" (Paso 4 Dominio implementado para usuarios) y revise la sección "**My Domain Settings**" (Mi configuración de dominio).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="e4c8b-174">![Dominio implementado al usuario](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Dominio implementado al usuario")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="e4c8b-175">En el sitio de la compañía de Jobscience, haga clic en **Security Controls** (Controles de seguridad) y, a continuación, haga clic en **Single Sign-On Settings** (Configuración de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="e4c8b-176">![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="e4c8b-177">En la sección **Configuración del inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="e4c8b-178">![Configuración de inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="e4c8b-179">a.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-179">a.</span></span> <span data-ttu-id="e4c8b-180">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="e4c8b-181">b.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-181">b.</span></span> <span data-ttu-id="e4c8b-182">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-182">Click **New**.</span></span>

13. <span data-ttu-id="e4c8b-183">En el cuadro de diálogo **SAML Single Sign-On Setting Edit** (Edición de la configuración de inicio de sesión único de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="e4c8b-184">![Inicio de sesión único SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="e4c8b-185">a.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-185">a.</span></span> <span data-ttu-id="e4c8b-186">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="e4c8b-187">b.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-187">b.</span></span> <span data-ttu-id="e4c8b-188">En el cuadro de texto **Emisor**, pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e4c8b-189">c.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-189">c.</span></span> <span data-ttu-id="e4c8b-190">En el cuadro de texto **Id. de identidad**, escriba `https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="e4c8b-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="e4c8b-191">d.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-191">d.</span></span> <span data-ttu-id="e4c8b-192">Haga clic en **Examinar** para cargar el certificado de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="e4c8b-193">e.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-193">e.</span></span> <span data-ttu-id="e4c8b-194">Como **SAML Identity Type** (Tipo de identidad SAML), seleccione **Assertion contains the Federation ID from the User object** (La aserción contiene el id. de federación del objeto Usuario).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="e4c8b-195">f.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-195">f.</span></span> <span data-ttu-id="e4c8b-196">Para **///SAML Identity Location** (Ubicación de identidad SAML), seleccione **///Identity is in the NameIdentfier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción Subject).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="e4c8b-197">g.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-197">g.</span></span> <span data-ttu-id="e4c8b-198">En el cuadro de texto **Identity Provider Login URL** (Dirección URL de inicio de sesión del proveedor de identidades), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e4c8b-199">h.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-199">h.</span></span> <span data-ttu-id="e4c8b-200">En el cuadro de texto **Identity Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades), pegue el valor de **dirección URL de cierre de sesión**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e4c8b-201">i.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-201">i.</span></span> <span data-ttu-id="e4c8b-202">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-202">Click **Save**.</span></span>

14. <span data-ttu-id="e4c8b-203">En el panel de navegación izquierdo, en la sección **Administer** (Administrar), haga clic en **Domain Management** (Administración de dominios) para expandir la sección relacionada y, luego, haga clic en **My Domain** (Mi dominio) para abrir la página **My Domain** (Mi dominio).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="e4c8b-204">![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="e4c8b-205">En la página **My domain** (Mi dominio), en la sección **Login Page Branding** (Personalización de marca de la página de inicio de sesión), haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="e4c8b-206">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="e4c8b-207">En la página **Login Page Branding** (Personalización de marca de la página de inicio de sesión), en la sección **Authentication Service** (Servicio de autenticación), se muestra el nombre de su **SAML SSO Settings** (Configuración de SSO de SAML).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="e4c8b-208">Selecciónelo y luego haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="e4c8b-209">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="e4c8b-210">Para obtener la dirección URL de inicio de sesión único iniciado por el proveedor de servicios, haga clic en **Configuración de inicio de sesión único** en la sección del menú **Controles de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="e4c8b-211">![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="e4c8b-212">Haga clic en el perfil SSO creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="e4c8b-213">En esta página se muestra la URL de inicio de sesión único de la empresa (por ejemplo, [https://nombreDeLaEmpresa.my.salesforce.com?so=idEmpresa](https://companyname.my.salesforce.com?so=companyid)).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="e4c8b-214">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e4c8b-215">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e4c8b-216">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e4c8b-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4c8b-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4c8b-218">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e4c8b-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e4c8b-220">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e4c8b-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4c8b-221">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4c8b-223">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4c8b-225">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4c8b-227">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4c8b-229">a.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-229">a.</span></span> <span data-ttu-id="e4c8b-230">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4c8b-231">b.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-231">b.</span></span> <span data-ttu-id="e4c8b-232">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4c8b-233">c.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-233">c.</span></span> <span data-ttu-id="e4c8b-234">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4c8b-235">d.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-235">d.</span></span> <span data-ttu-id="e4c8b-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="e4c8b-237">Creación de un usuario de prueba de Jobscience</span><span class="sxs-lookup"><span data-stu-id="e4c8b-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="e4c8b-238">Para permitir que los usuarios de Azure AD inicien sesión en Jobscience, deben aprovisionarse en Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="e4c8b-239">En el caso de Jobscience, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e4c8b-240">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Jobscience ofrecida por Jobscience para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="e4c8b-241">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="e4c8b-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e4c8b-242">Inicie sesión como administrador en el sitio de la compañía de **Jobscience** .</span><span class="sxs-lookup"><span data-stu-id="e4c8b-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="e4c8b-243">Vaya a Setup (Configuración).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-243">Go to Setup.</span></span>
   
   <span data-ttu-id="e4c8b-244">![Instalación](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="e4c8b-245">Vaya a **Manage Users \> (Administrar usuarios) Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="e4c8b-246">![Usuarios](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="e4c8b-247">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-247">Click **New User**.</span></span>
   
   <span data-ttu-id="e4c8b-248">![Todos los usuarios](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos los usuarios")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="e4c8b-249">En el cuadro de diálogo **Editar usuario** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e4c8b-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="e4c8b-250">![Edición de usuarios](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edición de usuarios")</span><span class="sxs-lookup"><span data-stu-id="e4c8b-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="e4c8b-251">a.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-251">a.</span></span> <span data-ttu-id="e4c8b-252">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, Britta.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="e4c8b-253">b.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-253">b.</span></span> <span data-ttu-id="e4c8b-254">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso, Simon.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="e4c8b-255">c.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-255">c.</span></span> <span data-ttu-id="e4c8b-256">En el cuadro de texto **Alias**, escriba el nombre del alias del usuario, como brittas.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="e4c8b-257">d.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-257">d.</span></span> <span data-ttu-id="e4c8b-258">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="e4c8b-259">e.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-259">e.</span></span> <span data-ttu-id="e4c8b-260">En el cuadro de texto **Nombre de usuario**, escriba un nombre de usuario como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="e4c8b-261">f.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-261">f.</span></span> <span data-ttu-id="e4c8b-262">En el cuadro de texto **Sobrenombre**, escriba un sobrenombre del usuario, como Simon.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="e4c8b-263">g.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-263">g.</span></span> <span data-ttu-id="e4c8b-264">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="e4c8b-265">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e4c8b-266">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4c8b-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e4c8b-267">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e4c8b-269">**Para asignar a Britta Simon a Jobscience, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e4c8b-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="e4c8b-270">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e4c8b-272">En la lista de aplicaciones, seleccione **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-272">In the applications list, select **Jobscience**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="e4c8b-274">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e4c8b-276">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-276">Click **Add** button.</span></span> <span data-ttu-id="e4c8b-277">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e4c8b-279">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e4c8b-280">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4c8b-281">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4c8b-282">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e4c8b-282">Testing single sign-on</span></span>

<span data-ttu-id="e4c8b-283">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e4c8b-284">Al hacer clic en el icono de Jobscience en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e4c8b-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="e4c8b-285">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4c8b-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4c8b-286">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e4c8b-286">Additional resources</span></span>

* [<span data-ttu-id="e4c8b-287">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4c8b-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4c8b-288">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e4c8b-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

