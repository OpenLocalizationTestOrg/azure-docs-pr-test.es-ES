---
title: "Tutorial: Integración de Azure Active Directory con TargetProcess | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="f5e6d-103">Tutorial: Integración de Azure Active Directory con TargetProcess</span><span class="sxs-lookup"><span data-stu-id="f5e6d-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="f5e6d-104">En este tutorial, aprenderá a integrar TargetProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5e6d-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5e6d-105">Integrar TargetProcess con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5e6d-106">Puede controlar en Azure AD quién tiene acceso a TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="f5e6d-107">Puede permitir que los usuarios inicien sesión automáticamente en TargetProcess (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5e6d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5e6d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5e6d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5e6d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f5e6d-110">Prerequisites</span></span>

<span data-ttu-id="f5e6d-111">Para configurar la integración de Azure AD con TargetProcess, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="f5e6d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5e6d-113">Una suscripción habilitada para inicio de sesión único en TargetProcess</span><span class="sxs-lookup"><span data-stu-id="f5e6d-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5e6d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5e6d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5e6d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5e6d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5e6d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5e6d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f5e6d-118">Scenario description</span></span>
<span data-ttu-id="f5e6d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5e6d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5e6d-121">Incorporación de TargetProcess desde la galería</span><span class="sxs-lookup"><span data-stu-id="f5e6d-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="f5e6d-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="f5e6d-123">Incorporación de TargetProcess desde la galería</span><span class="sxs-lookup"><span data-stu-id="f5e6d-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="f5e6d-124">Para configurar la integración de TargetProcess en Azure AD, deberá agregar TargetProcess desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5e6d-125">**Para agregar TargetProcess desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f5e6d-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e6d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5e6d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5e6d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f5e6d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f5e6d-133">En el cuadro de búsqueda, escriba **TargetProcess**, seleccione **TargetProcess** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![Incorporación de TargetProcess desde la galería](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f5e6d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f5e6d-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con TargetProcess con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5e6d-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5e6d-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TargetProcess para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="f5e6d-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="f5e6d-139">Para establecer la relación de vínculo, en TargetProcess, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5e6d-140">Para configurar y probar el inicio de sesión único de Azure AD con TargetProcess, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5e6d-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5e6d-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5e6d-143">**[Creación de un usuario de prueba de TargetProcess](#create-a-targetprocess-test-user)**: para tener un homólogo de Britta Simon en TargetProcess que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5e6d-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5e6d-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f5e6d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f5e6d-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="f5e6d-148">**Para configurar el inicio de sesión único de Azure AD con TargetProcess, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f5e6d-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e6d-149">En Azure Portal, en la página de integración de la aplicación **TargetProcess**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f5e6d-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="f5e6d-153">En la sección de **Dominio y direcciones URL de TargetProcess**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Sección Dominio y direcciones URL de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="f5e6d-155">a.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-155">a.</span></span> <span data-ttu-id="f5e6d-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.tpondemand.com/`.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="f5e6d-157">b.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-157">b.</span></span> <span data-ttu-id="f5e6d-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="f5e6d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5e6d-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-159">These values are not real.</span></span> <span data-ttu-id="f5e6d-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5e6d-161">Póngase en contacto con el [equipo de atención al cliente de TargetProcess](mailto:support@targetprocess.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f5e6d-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="f5e6d-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f5e6d-164">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5e6d-166">En la sección **Configuración de TargetProcess**, haga clic en **Configurar TargetProcess** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5e6d-167">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sección Configuración de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="f5e6d-169">Inicie sesión en su aplicación TargetProcess como administrador.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="f5e6d-170">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Configuración](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="f5e6d-172">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-172">Click **Settings**.</span></span>
   
    ![Configuración](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="f5e6d-174">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-174">Click **Single Sign-on**.</span></span>
   
    ![clic en Inicio de sesión único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="f5e6d-176">En el cuadro de diálogo Configuración de inicio de sesión único, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="f5e6d-178">a.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-178">a.</span></span> <span data-ttu-id="f5e6d-179">Haga lic en **Habilitar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="f5e6d-180">b.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-180">b.</span></span> <span data-ttu-id="f5e6d-181">En el cuadro de texto **Sign-on URL** (Dirección URL de inicio de sesión), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f5e6d-182">c.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-182">c.</span></span> <span data-ttu-id="f5e6d-183">Abra el certificado descargado en el Bloc de notas, copie el contenido y luego péguelo en el cuadro de texto **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="f5e6d-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="f5e6d-184">d.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-184">d.</span></span> <span data-ttu-id="f5e6d-185">Haga clic en **Habilitar aprovisionamiento de JIT**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="f5e6d-186">e.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-186">e.</span></span> <span data-ttu-id="f5e6d-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f5e6d-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5e6d-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5e6d-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5e6d-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f5e6d-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-191">Create an Azure AD test user</span></span>
<span data-ttu-id="f5e6d-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5e6d-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f5e6d-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f5e6d-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e6d-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5e6d-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Para mostrar la lista de usuarios](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5e6d-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5e6d-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f5e6d-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Sección Usuario](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5e6d-203">a.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-203">a.</span></span> <span data-ttu-id="f5e6d-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5e6d-205">b.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-205">b.</span></span> <span data-ttu-id="f5e6d-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5e6d-207">c.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-207">c.</span></span> <span data-ttu-id="f5e6d-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5e6d-209">d.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-209">d.</span></span> <span data-ttu-id="f5e6d-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="f5e6d-211">Creación de un usuario de prueba de TargetProcess</span><span class="sxs-lookup"><span data-stu-id="f5e6d-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="f5e6d-212">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="f5e6d-213">TargetProcess admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="f5e6d-214">Ya lo ha habilitado en [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="f5e6d-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="f5e6d-215">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f5e6d-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e6d-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="f5e6d-217">En esta sección, concederá acceso a Britta Simon a TargetProcess para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f5e6d-219">**Para asignar a Britta Simon a TargetProcess, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f5e6d-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e6d-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f5e6d-222">En la lista de aplicaciones, seleccione **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess en la lista de aplicaciones](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="f5e6d-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f5e6d-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-226">Click **Add** button.</span></span> <span data-ttu-id="f5e6d-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f5e6d-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5e6d-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5e6d-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f5e6d-232">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f5e6d-232">Test single sign-on</span></span>

<span data-ttu-id="f5e6d-233">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5e6d-234">Al hacer clic en el icono de TargetProcess en el panel de acceso, debería iniciar sesión automáticamente en su aplicación TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="f5e6d-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="f5e6d-235">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5e6d-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5e6d-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f5e6d-236">Additional resources</span></span>

* [<span data-ttu-id="f5e6d-237">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5e6d-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5e6d-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5e6d-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

