---
title: "Tutorial: Integración de Azure Active Directory con Google Apps en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="0d6a2-103">Tutorial: Integración de Azure Active Directory con Google Apps</span><span class="sxs-lookup"><span data-stu-id="0d6a2-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="0d6a2-104">En este tutorial, obtendrá información sobre cómo integrar Google Apps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d6a2-105">La integración de Google Apps con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d6a2-106">En Azure AD se puede controlar quién tiene acceso a Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="0d6a2-107">Puede permitir que los usuarios inicien sesión automáticamente en Google Apps (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d6a2-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0d6a2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d6a2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d6a2-110">Prerequisites</span></span>

<span data-ttu-id="0d6a2-111">Para configurar la integración de Azure AD con Google Apps, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="0d6a2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d6a2-113">Una suscripción habilitada para el inicio de sesión único en Google Apps</span><span class="sxs-lookup"><span data-stu-id="0d6a2-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d6a2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d6a2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d6a2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d6a2-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="0d6a2-118">Tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="0d6a2-118">Video tutorial</span></span>
<span data-ttu-id="0d6a2-119">Habilitación del inicio de sesión único en Google Apps en 2 minutos:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="0d6a2-120">Preguntas frecuentes</span><span class="sxs-lookup"><span data-stu-id="0d6a2-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="0d6a2-121">**P: ¿Son los Chromebooks y otros dispositivos Chrome compatibles con el inicio de sesión único de Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="0d6a2-122">R: Sí, los usuarios pueden iniciar sesión en sus dispositivos Chromebook con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="0d6a2-123">Consulte este [artículo de soporte técnico de Google Apps](https://support.google.com/chrome/a/answer/6060880) para información sobre por qué puede que se pidan las credenciales a los usuarios dos veces.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="0d6a2-124">**P: Si se habilita el inicio de sesión único, ¿podrán usar los usuarios sus credenciales de Azure AD para iniciar sesión en cualquier producto de Google, como Google Classroom, GMail, Google Drive, YouTube, etc.?**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="0d6a2-125">R: Sí, en función de [qué aplicaciones de Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) decida habilitar o deshabilitar para su organización.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="0d6a2-126">**P: ¿Puedo habilitar el inicio de sesión único solo para un subconjunto de mis usuarios de Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="0d6a2-127">R: No; si activa el inicio de sesión único, es necesario de inmediato que todos los usuarios de Google Apps se autentiquen con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="0d6a2-128">Dado que Google Apps no admite tener varios proveedores de identidades, el proveedor de identidades para su entorno de Google Apps puede ser Azure AD o Google, pero no ambos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="0d6a2-129">**P: Si un usuario inicia sesión a través de Windows, ¿se autentica automáticamente en Google Apps sin que se le pida una contraseña?**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="0d6a2-130">R: Hay dos opciones para habilitar este escenario.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="0d6a2-131">En primer lugar, los usuarios podrían iniciar sesión en dispositivos Windows 10 a través de [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="0d6a2-132">Como alternativa, los usuarios podrían iniciar sesión en dispositivos Windows que están unidos a un dominio en un entorno Active Directory local que se ha habilitado para el inicio de sesión único en Azure AD a través de una implementación de los [Servicios de federación de Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) .</span><span class="sxs-lookup"><span data-stu-id="0d6a2-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="0d6a2-133">Ambas opciones requieren que realice los pasos del tutorial siguiente para permitir el inicio de sesión único entre Azure AD y Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d6a2-134">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0d6a2-134">Scenario description</span></span>
<span data-ttu-id="0d6a2-135">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d6a2-136">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d6a2-137">Incorporación de Google Apps desde la galería</span><span class="sxs-lookup"><span data-stu-id="0d6a2-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="0d6a2-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="0d6a2-139">Incorporación de Google Apps desde la galería</span><span class="sxs-lookup"><span data-stu-id="0d6a2-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="0d6a2-140">Para configurar la integración de Google Apps en Azure AD, será preciso que agregue Google Apps desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d6a2-141">**Para agregar Google Apps desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d6a2-142">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d6a2-144">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d6a2-145">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-145">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0d6a2-147">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0d6a2-149">En el cuadro de búsqueda, escriba **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-149">In the search box, type **Google Apps**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="0d6a2-151">En el panel de resultados, seleccione **Google Apps** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d6a2-153">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d6a2-154">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Google Apps con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d6a2-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0d6a2-155">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Google Apps para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="0d6a2-156">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="0d6a2-157">Para establecer la relación de vínculo, en Google Apps, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="0d6a2-158">Para configurar y probar el inicio de sesión único de Azure AD con Google Apps, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d6a2-159">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d6a2-160">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d6a2-161">**[Creación de un usuario de prueba de Google Apps](#creating-a-google-apps-test-user)**: para tener un homólogo de Britta Simon en Google Apps que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d6a2-162">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d6a2-163">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d6a2-164">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d6a2-165">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="0d6a2-166">**Para configurar el inicio de sesión único de Azure AD con Google Apps, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="0d6a2-167">En Azure Portal, en la página de integración de la aplicación **Google Apps**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0d6a2-169">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="0d6a2-171">En la sección de **dominio y direcciones URL de Google Apps**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="0d6a2-173">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://mail.google.com/a/<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0d6a2-174">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-174">This value is not real.</span></span> <span data-ttu-id="0d6a2-175">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="0d6a2-176">póngase en contacto con el [equipo de soporte técnico de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="0d6a2-177">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="0d6a2-179">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0d6a2-179">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d6a2-181">En la sección **Configuración de Google Apps**, haga clic en **Configurar Google Apps** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d6a2-182">Copie la **dirección URL de cierre de sesión, la dirección URL del servicio de inicio de sesión único de SAML y la dirección URL de cambio de contraseña** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="0d6a2-184">Abra una nueva pestaña en el explorador e inicie sesión en la [consola de administración de Google Apps](http://admin.google.com/) con su cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="0d6a2-185">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-185">Click **Security**.</span></span> <span data-ttu-id="0d6a2-186">Si no ve el vínculo, puede estar oculto debajo del menú **Más controles** en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Haga clic en Seguridad.][10]

9. <span data-ttu-id="0d6a2-188">En la página **Seguridad**, haga clic en **Configurar inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Haga clic en SSO.][11]

10. <span data-ttu-id="0d6a2-190">Realice los cambios de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-190">Perform the following configuration changes:</span></span>
   
    ![Configuración de SSO][12]
   
    <span data-ttu-id="0d6a2-192">a.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-192">a.</span></span> <span data-ttu-id="0d6a2-193">Seleccione **Configurar SSO con un proveedor de identidades de terceros**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="0d6a2-194">b.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-194">b.</span></span> <span data-ttu-id="0d6a2-195">En el campo **Dirección URL de la página de inicio de sesión** en Google Apps, pegue el valor de la **dirección URL del servicio de inicio de sesión único** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0d6a2-196">c.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-196">c.</span></span> <span data-ttu-id="0d6a2-197">En el campo **Dirección URL de cierre de sesión** en Google Apps, pegue el valor de la **dirección URL de cierre de sesión** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0d6a2-198">d.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-198">d.</span></span> <span data-ttu-id="0d6a2-199">En el campo **Dirección URL de cambio de contraseña** en Google Apps, pegue el valor de la **dirección URL de cambio de contraseña** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0d6a2-200">e.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-200">e.</span></span> <span data-ttu-id="0d6a2-201">En Google Apps, para el **certificado de comprobación**, cargue el certificado que descargó de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="0d6a2-202">f.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-202">f.</span></span> <span data-ttu-id="0d6a2-203">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0d6a2-204">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0d6a2-205">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0d6a2-206">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d6a2-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d6a2-207">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d6a2-208">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d6a2-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0d6a2-210">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d6a2-211">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d6a2-213">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d6a2-215">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d6a2-217">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0d6a2-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d6a2-219">a.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-219">a.</span></span> <span data-ttu-id="0d6a2-220">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d6a2-221">b.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-221">b.</span></span> <span data-ttu-id="0d6a2-222">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d6a2-223">c.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-223">c.</span></span> <span data-ttu-id="0d6a2-224">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0d6a2-225">d.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-225">d.</span></span> <span data-ttu-id="0d6a2-226">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="0d6a2-227">Creación de un usuario de prueba de Google Apps</span><span class="sxs-lookup"><span data-stu-id="0d6a2-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="0d6a2-228">El objetivo de esta sección es crear un usuario llamado Britta Simon en Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="0d6a2-229">Google Apps admite el aprovisionamiento automático, que está habilitado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="0d6a2-230">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-230">There is no action for you in this section.</span></span> <span data-ttu-id="0d6a2-231">Si el usuario aún no existe en Google Apps Software, se crea uno nuevo cuando se intenta acceder a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="0d6a2-232">Si necesita crear manualmente un usuario, póngase en contacto con el [equipo de soporte técnico de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0d6a2-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0d6a2-233">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d6a2-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0d6a2-234">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0d6a2-236">**Para asignar Britta Simon a Google Apps, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d6a2-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="0d6a2-237">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0d6a2-239">En la lista de aplicaciones, seleccione **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-239">In the applications list, select **Google Apps**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="0d6a2-241">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0d6a2-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-243">Click **Add** button.</span></span> <span data-ttu-id="0d6a2-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0d6a2-246">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d6a2-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d6a2-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d6a2-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0d6a2-249">Testing single sign-on</span></span>

<span data-ttu-id="0d6a2-250">En esta sección, para probar la configuración del inicio de sesión único, abra el Panel de acceso en [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)y, a continuación, inicie sesión en la cuenta de prueba y haga clic en el icono **Google Apps** en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0d6a2-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d6a2-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d6a2-251">Additional resources</span></span>

* [<span data-ttu-id="0d6a2-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d6a2-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d6a2-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d6a2-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0d6a2-254">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="0d6a2-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png