---
title: "Tutorial: integración de Azure Active Directory con SuccessFactors | Microsoft Docs"
description: "Aprenda cómo usar SuccessFactors con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="47725-103">Tutorial: integración de Azure Active Directory con SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="47725-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="47725-104">El objetivo de este tutorial es mostrar cómo integrar SuccessFactors con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47725-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47725-105">La integración de SuccessFactors con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="47725-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="47725-106">Puede controlar en Azure AD quién tiene acceso a SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="47725-107">Puede permitir que los usuarios inicien sesión automáticamente en SuccessFactors(inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="47725-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47725-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="47725-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47725-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47725-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47725-110">Prerequisites</span></span>
<span data-ttu-id="47725-111">Para configurar la integración de Azure AD con SuccessFactors, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="47725-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="47725-112">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="47725-112">A valid Azure subscription</span></span>
* <span data-ttu-id="47725-113">Un inquilino en SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="47725-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="47725-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="47725-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="47725-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="47725-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="47725-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="47725-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="47725-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47725-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47725-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="47725-118">Scenario description</span></span>
<span data-ttu-id="47725-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="47725-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="47725-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="47725-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47725-121">Incorporación de SuccessFactors desde la galería</span><span class="sxs-lookup"><span data-stu-id="47725-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="47725-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47725-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="47725-123">Incorporación de SuccessFactors desde la galería</span><span class="sxs-lookup"><span data-stu-id="47725-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="47725-124">Para configurar la integración de SuccessFactors en Azure AD, deberá agregar SuccessFactors desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="47725-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="47725-125">**Para agregar SuccessFactors desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="47725-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="47725-126">En el Portal de Azure clásico, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47725-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Configuración del inicio de sesión único][1]
2. <span data-ttu-id="47725-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="47725-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="47725-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="47725-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configuración del inicio de sesión único][2]
4. <span data-ttu-id="47725-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="47725-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="47725-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="47725-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configuración del inicio de sesión único][4]
6. <span data-ttu-id="47725-135">En el **cuadro de búsqueda**, escriba **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="47725-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Configuración del inicio de sesión único][5]
7. <span data-ttu-id="47725-137">En el panel de resultados, seleccione **SuccessFactors** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47725-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Configuración del inicio de sesión único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47725-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47725-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47725-140">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con SuccessFactors con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47725-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47725-141">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SuccessFactors para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="47725-142">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="47725-143">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="47725-144">Para configurar y probar el inicio de sesión único de Azure AD con SuccessFactors, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="47725-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="47725-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="47725-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="47725-146">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47725-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47725-147">**[Creación de un usuario de prueba de SuccessFactors](#creating-a-successfactors-test-user)** : para tener un homólogo de Britta Simon en SuccessFactors que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="47725-148">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47725-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="47725-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47725-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47725-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="47725-151">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal clásico y configurará el inicio de sesión único en la aplicación SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="47725-152">**Para configurar el inicio de sesión único de Azure AD con SuccessFactors, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="47725-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="47725-153">En el Portal de Azure clásico, en la página de integración de aplicaciones de **SuccessFactors**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="47725-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Configuración del inicio de sesión único][7]
2. <span data-ttu-id="47725-155">En la página **¿Cómo desea que los usuarios inicien sesión en SuccessFactors?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47725-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configuración del inicio de sesión único][8]
3. <span data-ttu-id="47725-157">En la página **Configurar dirección URL de la aplicación**, realice los pasos siguientes y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47725-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Configuración del inicio de sesión único][9]
   
    <span data-ttu-id="47725-159">a.</span><span class="sxs-lookup"><span data-stu-id="47725-159">a.</span></span> <span data-ttu-id="47725-160">En el cuadro de texto **URL de inicio de sesión** , escriba una dirección URL con uno de los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="47725-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="47725-161">b.</span><span class="sxs-lookup"><span data-stu-id="47725-161">b.</span></span> <span data-ttu-id="47725-162">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con uno de los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="47725-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="47725-163">c.</span><span class="sxs-lookup"><span data-stu-id="47725-163">c.</span></span> <span data-ttu-id="47725-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47725-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="47725-165">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="47725-165">Please note that these are not the real values.</span></span> <span data-ttu-id="47725-166">Tendrá que actualizar estos valores con la dirección URL de inicio de sesión y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="47725-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="47725-167">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="47725-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="47725-168">En la página **Configurar inicio de sesión único en SuccessFactors**, haga clic en **Descargar certificado** y guarde el archivo de certificado localmente en su equipo.</span><span class="sxs-lookup"><span data-stu-id="47725-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configuración del inicio de sesión único][10]

2. <span data-ttu-id="47725-170">En otra ventana del explorador web, inicie sesión en el **Portal de administración de SuccessFactors** como administrador.</span><span class="sxs-lookup"><span data-stu-id="47725-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="47725-171">Visite **Application Security** (Seguridad de aplicaciones) y establezca nativo en **Single Sign On Features** (Características de Inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="47725-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="47725-172">Coloque cualquier valor en **Reset Token** (Restablecer Token) y haga clic en **Save Token** (Guardar Token) para habilitar SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="47725-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][11]

    > [!NOTE] 
    > <span data-ttu-id="47725-174">Este valor solo se utiliza como el conmutador de activado y desactivado.</span><span class="sxs-lookup"><span data-stu-id="47725-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="47725-175">Si se guarda algún valor, el SSO de SAML está activado.</span><span class="sxs-lookup"><span data-stu-id="47725-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="47725-176">Si se guarda un valor en blanco, el SSO de SAML está desactivado.</span><span class="sxs-lookup"><span data-stu-id="47725-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="47725-177">Vaya a la siguiente captura de pantalla y realice las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="47725-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][12]
   
    <span data-ttu-id="47725-179">a.</span><span class="sxs-lookup"><span data-stu-id="47725-179">a.</span></span> <span data-ttu-id="47725-180">Seleccione el botón de selección **SAML v2 SSO** (SSO de SAML v2).</span><span class="sxs-lookup"><span data-stu-id="47725-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="47725-181">b.</span><span class="sxs-lookup"><span data-stu-id="47725-181">b.</span></span> <span data-ttu-id="47725-182">Establezca nombre de entidad asertivo de SAML (emisor de SAml + nombre de la empresa).</span><span class="sxs-lookup"><span data-stu-id="47725-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="47725-183">c.</span><span class="sxs-lookup"><span data-stu-id="47725-183">c.</span></span> <span data-ttu-id="47725-184">En el cuadro de texto **SAML Issuer** (Emisor de SAML), coloque el valor de **URL del emisor** del Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="47725-185">d.</span><span class="sxs-lookup"><span data-stu-id="47725-185">d.</span></span> <span data-ttu-id="47725-186">Seleccione **Response(Customer Generated/IdP/AP)** [Respuesta (cliente generado/IdP/AP)] como **Require Mandatory Signature** (Requerir firma obligatoria).</span><span class="sxs-lookup"><span data-stu-id="47725-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="47725-187">e.</span><span class="sxs-lookup"><span data-stu-id="47725-187">e.</span></span> <span data-ttu-id="47725-188">Seleccione **Enabled** (Habilitado) como **Enable SAML Flag** (Habilitar marca SAML).</span><span class="sxs-lookup"><span data-stu-id="47725-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="47725-189">f.</span><span class="sxs-lookup"><span data-stu-id="47725-189">f.</span></span> <span data-ttu-id="47725-190">Seleccione **No** como **Login Request Signature(SF Generated/SP/RP)** [Firma de solicitud de inicio de sesión (SF generado/SP/RP)].</span><span class="sxs-lookup"><span data-stu-id="47725-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="47725-191">g.</span><span class="sxs-lookup"><span data-stu-id="47725-191">g.</span></span> <span data-ttu-id="47725-192">Seleccione **Browser/Post Profile** (Perfil de explorador/envío) como **SAML Profile** (Perfil SAML).</span><span class="sxs-lookup"><span data-stu-id="47725-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="47725-193">h.</span><span class="sxs-lookup"><span data-stu-id="47725-193">h.</span></span> <span data-ttu-id="47725-194">Seleccione **No** como **Enforce Certificate Valid Period** (Aplicar período válido de certificado).</span><span class="sxs-lookup"><span data-stu-id="47725-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="47725-195">i.</span><span class="sxs-lookup"><span data-stu-id="47725-195">i.</span></span> <span data-ttu-id="47725-196">Copie el contenido del archivo de certificado descargado y péguelo en el cuadro de texto **SAML Verifying Certificate** (Certificado de verificación de firma).</span><span class="sxs-lookup"><span data-stu-id="47725-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47725-197">El contenido del certificado debe tener etiquetas de inicio y fin del certificado.</span><span class="sxs-lookup"><span data-stu-id="47725-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="47725-198">Vaya a SAML V2 y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47725-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][13]
   
    <span data-ttu-id="47725-200">a.</span><span class="sxs-lookup"><span data-stu-id="47725-200">a.</span></span> <span data-ttu-id="47725-201">Seleccione **Yes** (Sí) como **Support SP-initiated Global Logout** (Permitir cierre de sesión global iniciado por SP).</span><span class="sxs-lookup"><span data-stu-id="47725-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="47725-202">b.</span><span class="sxs-lookup"><span data-stu-id="47725-202">b.</span></span> <span data-ttu-id="47725-203">En el cuadro de texto **Global Logout Service URL (LogoutRequest destination)** [URL del servicio de cierre de sesión global (destino de LogoutRequest)], coloque el valor de **Dirección de URL de cierre de sesión remoto** del Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="47725-204">c.</span><span class="sxs-lookup"><span data-stu-id="47725-204">c.</span></span> <span data-ttu-id="47725-205">Seleccione **No** en **Require sp must encrypt all NameID element** (Requerir que sp cifre todos los elementos NameID).</span><span class="sxs-lookup"><span data-stu-id="47725-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="47725-206">d.</span><span class="sxs-lookup"><span data-stu-id="47725-206">d.</span></span> <span data-ttu-id="47725-207">Seleccione **Unspecified** (Sin especificar) como **NameID Format** (Formato de NameID).</span><span class="sxs-lookup"><span data-stu-id="47725-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="47725-208">e.</span><span class="sxs-lookup"><span data-stu-id="47725-208">e.</span></span> <span data-ttu-id="47725-209">Seleccione **Yes** (Sí) como **Enable sp initiated login (AuthnRequest)** [Permitir inicio de sesión iniciado por sp (AuthnRequest)].</span><span class="sxs-lookup"><span data-stu-id="47725-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="47725-210">f.</span><span class="sxs-lookup"><span data-stu-id="47725-210">f.</span></span> <span data-ttu-id="47725-211">En el cuadro de texto **Send request as Company-Wide issuer** (Enviar solicitud como emisor en toda la empresa), coloque el valor de **Dirección URL de inicio de sesión remoto** del Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47725-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="47725-212">Siga estos pasos si desea que los nombres de usuario de inicio de sesión no distingan mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="47725-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="47725-213">a.</span><span class="sxs-lookup"><span data-stu-id="47725-213">a.</span></span> <span data-ttu-id="47725-214">Visite **Company Settings**(Configuración de la empresa) en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="47725-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="47725-215">b.</span><span class="sxs-lookup"><span data-stu-id="47725-215">b.</span></span> <span data-ttu-id="47725-216">Seleccione la casilla junto a **Enable Non-Case-Sensitive Username**(Habilitar nombre de usuario sin distinción de mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="47725-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="47725-217">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="47725-217">c.Click **Save**.</span></span>
   
    ![Configurar inicio de sesión único][29]

    > [!NOTE] 
    > <span data-ttu-id="47725-219">Si intenta habilitar esta opción, el sistema comprueba si creará un nombre de inicio de sesión de SAML duplicado.</span><span class="sxs-lookup"><span data-stu-id="47725-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="47725-220">Por ejemplo, si el cliente tiene nombres de usuario User1 y user1.</span><span class="sxs-lookup"><span data-stu-id="47725-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="47725-221">Al no distinguir mayúsculas de minúsculas, estos nombres pasan a ser duplicados.</span><span class="sxs-lookup"><span data-stu-id="47725-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="47725-222">El sistema mostrará un mensaje de error y no se habilitará la característica.</span><span class="sxs-lookup"><span data-stu-id="47725-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="47725-223">El cliente deberá cambiar uno de los nombres de usuario, para que realmente esté escrito diferente.</span><span class="sxs-lookup"><span data-stu-id="47725-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="47725-224">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="47725-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Aplicaciones][14]
2. <span data-ttu-id="47725-226">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="47725-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplicaciones][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47725-228">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47725-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="47725-229">El objetivo de esta sección es crear un usuario de prueba en el Portal clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47725-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][16]

<span data-ttu-id="47725-231">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="47725-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="47725-232">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47725-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][17]
2. <span data-ttu-id="47725-234">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="47725-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="47725-235">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="47725-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][18]
4. <span data-ttu-id="47725-237">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="47725-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][19]
5. <span data-ttu-id="47725-239">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47725-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][20]
   
    <span data-ttu-id="47725-241">a.</span><span class="sxs-lookup"><span data-stu-id="47725-241">a.</span></span> <span data-ttu-id="47725-242">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="47725-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="47725-243">b.</span><span class="sxs-lookup"><span data-stu-id="47725-243">b.</span></span> <span data-ttu-id="47725-244">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47725-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="47725-245">c.</span><span class="sxs-lookup"><span data-stu-id="47725-245">c.</span></span> <span data-ttu-id="47725-246">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47725-246">Click **Next**.</span></span>
6. <span data-ttu-id="47725-247">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47725-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][21]
   
    <span data-ttu-id="47725-249">a.</span><span class="sxs-lookup"><span data-stu-id="47725-249">a.</span></span> <span data-ttu-id="47725-250">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="47725-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="47725-251">b.</span><span class="sxs-lookup"><span data-stu-id="47725-251">b.</span></span> <span data-ttu-id="47725-252">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="47725-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="47725-253">c.</span><span class="sxs-lookup"><span data-stu-id="47725-253">c.</span></span> <span data-ttu-id="47725-254">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47725-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="47725-255">d.</span><span class="sxs-lookup"><span data-stu-id="47725-255">d.</span></span> <span data-ttu-id="47725-256">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="47725-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="47725-257">e.</span><span class="sxs-lookup"><span data-stu-id="47725-257">e.</span></span> <span data-ttu-id="47725-258">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47725-258">Click **Next**.</span></span>
7. <span data-ttu-id="47725-259">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="47725-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][22]
8. <span data-ttu-id="47725-261">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47725-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][23]
   
    <span data-ttu-id="47725-263">a.</span><span class="sxs-lookup"><span data-stu-id="47725-263">a.</span></span> <span data-ttu-id="47725-264">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="47725-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="47725-265">b.</span><span class="sxs-lookup"><span data-stu-id="47725-265">b.</span></span> <span data-ttu-id="47725-266">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="47725-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="47725-267">Creación de un usuario de prueba de SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="47725-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="47725-268">Para permitir que los usuarios de Azure AD inicien sesión en SuccessFactors, deben aprovisionarse en SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="47725-269">En el caso de SuccessFactors, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="47725-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="47725-270">Para que se creen los usuarios en SuccessFactors, deberá ponerse en contacto con el [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="47725-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="47725-271">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47725-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="47725-272">El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure, para lo que se le concederá acceso a SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Asignar usuario][24]

<span data-ttu-id="47725-274">**Para asignar Britta Simon a SuccessFactors, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="47725-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="47725-275">En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="47725-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Asignar usuario][25]
2. <span data-ttu-id="47725-277">En la lista de aplicaciones, seleccione **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="47725-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Configurar inicio de sesión único][26]
3. <span data-ttu-id="47725-279">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="47725-279">In the menu on the top, click **Users**.</span></span>
   
    ![Asignar usuario][27]
4. <span data-ttu-id="47725-281">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47725-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="47725-282">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="47725-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="47725-284">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="47725-284">Testing single sign-on</span></span>
<span data-ttu-id="47725-285">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="47725-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="47725-286">Al hacer clic en el icono de SuccessFactors en el panel de acceso, debería iniciar sesión automáticamente en la aplicación SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="47725-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47725-287">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="47725-287">Additional resources</span></span>
* [<span data-ttu-id="47725-288">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47725-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47725-289">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47725-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
