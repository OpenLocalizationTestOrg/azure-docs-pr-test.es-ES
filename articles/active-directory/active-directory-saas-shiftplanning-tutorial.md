---
title: "Tutorial: Integración de Azure Active Directory con Humanity | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="4d72f-103">Tutorial: Integración de Azure Active Directory con Humanity</span><span class="sxs-lookup"><span data-stu-id="4d72f-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="4d72f-104">En este tutorial, aprenderá a integrar Humanity con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d72f-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d72f-105">La integración de Humanity con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4d72f-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d72f-106">Puede controlar en Azure AD quién tiene acceso a Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="4d72f-107">Puede permitir que los usuarios inicien sesión automáticamente en Humanity (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d72f-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d72f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d72f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4d72f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d72f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d72f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d72f-110">Prerequisites</span></span>

<span data-ttu-id="4d72f-111">Para configurar la integración de Azure AD con Humanity, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4d72f-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="4d72f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d72f-113">Una suscripción habilitada para el inicio de sesión único en Humanity</span><span class="sxs-lookup"><span data-stu-id="4d72f-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d72f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4d72f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d72f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4d72f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d72f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4d72f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d72f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d72f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d72f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4d72f-118">Scenario description</span></span>
<span data-ttu-id="4d72f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4d72f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d72f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4d72f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d72f-121">Adición de Humanity desde la galería</span><span class="sxs-lookup"><span data-stu-id="4d72f-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="4d72f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="4d72f-123">Adición de Humanity desde la galería</span><span class="sxs-lookup"><span data-stu-id="4d72f-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="4d72f-124">Para configurar la integración de Humanity en Azure AD, deberá agregar Humanity desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4d72f-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d72f-125">**Para agregar Humanity desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d72f-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d72f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d72f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d72f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4d72f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d72f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4d72f-133">En el cuadro de búsqueda, escriba **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-133">In the search box, type **Humanity**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="4d72f-135">En el panel de resultados, seleccione **Humanity** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d72f-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d72f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d72f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Humanity con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d72f-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d72f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Humanity para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d72f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="4d72f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="4d72f-141">Para establecer la relación de vínculo, en Humanity, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4d72f-142">Para configurar y probar el inicio de sesión único de Azure AD con Humanity, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4d72f-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d72f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="4d72f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d72f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d72f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d72f-145">**[Creación de un usuario de prueba de Humanity](#creating-a-humanity-test-user)**: el objetivo es tener un homólogo de Britta Simon en Humanity que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d72f-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d72f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d72f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d72f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d72f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d72f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d72f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="4d72f-150">**Para configurar el inicio de sesión único de Azure AD con Humanity, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d72f-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="4d72f-151">En la página de integración de la aplicación **Humanity** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4d72f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4d72f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="4d72f-155">En la sección **Dominio y direcciones URL de Humanity**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4d72f-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="4d72f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4d72f-157">a.</span></span> <span data-ttu-id="4d72f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://company.humanity.com/includes/saml/`.</span><span class="sxs-lookup"><span data-stu-id="4d72f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="4d72f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4d72f-159">b.</span></span> <span data-ttu-id="4d72f-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="4d72f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d72f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4d72f-161">These values are not real.</span></span> <span data-ttu-id="4d72f-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4d72f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4d72f-163">Póngase en contacto con el [equipo de soporte de cliente de Humanity](https://www.humanity.com/support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="4d72f-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="4d72f-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4d72f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="4d72f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4d72f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d72f-168">En la sección **Configuración de Humanity**, haga clic en **Configurar Humanity** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4d72f-169">Copie la **dirección URL del servicio de inicio de sesión único de SAML y la URL de cierre de sesión** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="4d72f-171">En otra ventana del explorador web, inicie sesión en el sitio de **Humanity** de la compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="4d72f-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="4d72f-172">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="4d72f-173">![Administración](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="4d72f-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="4d72f-174">En **Integración**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="4d72f-175">![Inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4d72f-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="4d72f-176">En la sección **Inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4d72f-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4d72f-177">![Inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4d72f-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="4d72f-178">a.</span><span class="sxs-lookup"><span data-stu-id="4d72f-178">a.</span></span> <span data-ttu-id="4d72f-179">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="4d72f-180">b.</span><span class="sxs-lookup"><span data-stu-id="4d72f-180">b.</span></span> <span data-ttu-id="4d72f-181">Seleccione **Allow Password Login** (Permitir inicio de sesión de contraseña).</span><span class="sxs-lookup"><span data-stu-id="4d72f-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="4d72f-182">c.</span><span class="sxs-lookup"><span data-stu-id="4d72f-182">c.</span></span> <span data-ttu-id="4d72f-183">Pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** en el cuadro de texto **SAML Issuer URL** (URL de emisor de SAML).</span><span class="sxs-lookup"><span data-stu-id="4d72f-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="4d72f-184">d.</span><span class="sxs-lookup"><span data-stu-id="4d72f-184">d.</span></span> <span data-ttu-id="4d72f-185">Peque el valor de **URL de cierre de sesión** en el cuadro de texto **Remote Logout URL** (URL de cierre de sesión remoto).</span><span class="sxs-lookup"><span data-stu-id="4d72f-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="4d72f-186">e.</span><span class="sxs-lookup"><span data-stu-id="4d72f-186">e.</span></span> <span data-ttu-id="4d72f-187">Abra el certificado codificado en base 64 en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="4d72f-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="4d72f-188">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="4d72f-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d72f-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4d72f-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4d72f-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4d72f-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d72f-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d72f-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d72f-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d72f-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4d72f-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4d72f-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d72f-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d72f-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d72f-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d72f-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d72f-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4d72f-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d72f-204">a.</span><span class="sxs-lookup"><span data-stu-id="4d72f-204">a.</span></span> <span data-ttu-id="4d72f-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d72f-206">b.</span><span class="sxs-lookup"><span data-stu-id="4d72f-206">b.</span></span> <span data-ttu-id="4d72f-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d72f-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d72f-208">c.</span><span class="sxs-lookup"><span data-stu-id="4d72f-208">c.</span></span> <span data-ttu-id="4d72f-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4d72f-210">d.</span><span class="sxs-lookup"><span data-stu-id="4d72f-210">d.</span></span> <span data-ttu-id="4d72f-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="4d72f-212">Creación de un usuario de prueba de Humanity</span><span class="sxs-lookup"><span data-stu-id="4d72f-212">Creating a Humanity test user</span></span>

<span data-ttu-id="4d72f-213">Para permitir que los usuarios de Azure AD inicien sesión en Humanity, deben aprovisionarse en Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="4d72f-214">En el caso de Humanity, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="4d72f-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="4d72f-215">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="4d72f-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4d72f-216">Inicie sesión en su sitio de la compañía de **Humanity** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4d72f-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="4d72f-217">Haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="4d72f-218">![Administración](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="4d72f-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="4d72f-219">Haga clic en **Personal**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="4d72f-220">![Personal](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Personal")</span><span class="sxs-lookup"><span data-stu-id="4d72f-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="4d72f-221">En **Acciones**, haga clic en **Agregar empleados**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="4d72f-222">![Agregar empleados](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Agregar empleados")</span><span class="sxs-lookup"><span data-stu-id="4d72f-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="4d72f-223">En la sección **Agregar empleados** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4d72f-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4d72f-224">![Guardar empleados](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Guardar empleados")</span><span class="sxs-lookup"><span data-stu-id="4d72f-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="4d72f-225">a.</span><span class="sxs-lookup"><span data-stu-id="4d72f-225">a.</span></span> <span data-ttu-id="4d72f-226">Escriba los datos de una cuenta de AAD válida que desee aprovisionar en los cuadros de texto correspondientes: **Nombre**, **Apellidos** y **Correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="4d72f-227">b.</span><span class="sxs-lookup"><span data-stu-id="4d72f-227">b.</span></span> <span data-ttu-id="4d72f-228">Haga clic en **Guardar empleados**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="4d72f-229">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Humanity que proporcione Humanity para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="4d72f-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4d72f-230">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d72f-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4d72f-231">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4d72f-233">**Para asignar a Britta Simon a Humanity, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d72f-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="4d72f-234">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4d72f-236">En la lista de aplicaciones, seleccione **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-236">In the applications list, select **Humanity**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="4d72f-238">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4d72f-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-240">Click **Add** button.</span></span> <span data-ttu-id="4d72f-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4d72f-243">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4d72f-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d72f-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d72f-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4d72f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d72f-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4d72f-246">Testing single sign-on</span></span>

<span data-ttu-id="4d72f-247">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4d72f-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4d72f-248">Al hacer clic en el icono de Humanity en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Humanity.</span><span class="sxs-lookup"><span data-stu-id="4d72f-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="4d72f-249">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d72f-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d72f-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4d72f-250">Additional resources</span></span>

* [<span data-ttu-id="4d72f-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d72f-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d72f-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d72f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

