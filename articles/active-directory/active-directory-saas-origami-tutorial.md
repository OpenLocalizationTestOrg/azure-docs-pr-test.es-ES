---
title: "Tutorial: Integración de Azure Active Directory con Origami | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="bdefd-103">Tutorial: Integración de Azure Active Directory con Origami</span><span class="sxs-lookup"><span data-stu-id="bdefd-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="bdefd-104">En este tutorial, obtendrá información sobre cómo integrar Origami con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdefd-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdefd-105">Integrar Origami con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bdefd-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bdefd-106">Puede controlar en Azure AD quién tiene acceso a Origami</span><span class="sxs-lookup"><span data-stu-id="bdefd-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="bdefd-107">Puede permitir que los usuarios inicien sesión automáticamente en Origami (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdefd-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdefd-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bdefd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bdefd-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdefd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdefd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bdefd-110">Prerequisites</span></span>

<span data-ttu-id="bdefd-111">Para configurar la integración de Azure AD con Origami, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bdefd-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="bdefd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdefd-113">Una suscripción habilitada para el inicio de sesión único en Pantheon</span><span class="sxs-lookup"><span data-stu-id="bdefd-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdefd-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bdefd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdefd-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bdefd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdefd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bdefd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdefd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdefd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdefd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bdefd-118">Scenario description</span></span>
<span data-ttu-id="bdefd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bdefd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdefd-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="bdefd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdefd-121">Incorporación de Origami desde la galería</span><span class="sxs-lookup"><span data-stu-id="bdefd-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="bdefd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="bdefd-123">Incorporación de Origami desde la galería</span><span class="sxs-lookup"><span data-stu-id="bdefd-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="bdefd-124">Para configurar la integración de Origami en Azure AD, deberá agregar Origami desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="bdefd-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bdefd-125">**Para agregar Origami desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bdefd-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bdefd-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdefd-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bdefd-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bdefd-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bdefd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bdefd-133">En el cuadro de búsqueda, escriba **Origami**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-133">In the search box, type **Origami**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="bdefd-135">En el panel de resultados, seleccione **Pantheon** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bdefd-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdefd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdefd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Origami con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bdefd-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdefd-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Origami para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdefd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="bdefd-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Origami.</span><span class="sxs-lookup"><span data-stu-id="bdefd-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="bdefd-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Pantheon.</span><span class="sxs-lookup"><span data-stu-id="bdefd-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bdefd-142">Para configurar y probar el inicio de sesión único de Azure AD con Origami, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bdefd-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bdefd-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="bdefd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bdefd-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdefd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdefd-145">**[Creación de un usuario de prueba de Origami](#creating-an-origami-test-user)**: el objetivo es tener un homólogo de Britta Simon en Origami que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdefd-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdefd-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdefd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdefd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bdefd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdefd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdefd-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Origami.</span><span class="sxs-lookup"><span data-stu-id="bdefd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="bdefd-150">**Para configurar el inicio de sesión único de Azure AD con Origami, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bdefd-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="bdefd-151">En la página de integración de la aplicación **Origami** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bdefd-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bdefd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="bdefd-155">En la sección **Dominio y direcciones URL de Origami** , lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bdefd-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="bdefd-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://live.origamirisk.com/origami/account/login?account=<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="bdefd-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdefd-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="bdefd-158">The value is not real.</span></span> <span data-ttu-id="bdefd-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="bdefd-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="bdefd-160">Póngase en contacto con el [equipo de atención al cliente de Origami ](https://wordpress.org/support/theme/origami) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="bdefd-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="bdefd-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bdefd-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="bdefd-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bdefd-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bdefd-165">En la sección **Configuración de Origami** , haga clic en **Configurar Origami**  para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bdefd-166">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="bdefd-168">Inicie sesión en la cuenta de Origami con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="bdefd-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="bdefd-169">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="bdefd-171">En la página del cuadro de diálogo Single Sign On Setup (Configuración de inicio de sesión único), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bdefd-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="bdefd-173">a.</span><span class="sxs-lookup"><span data-stu-id="bdefd-173">a.</span></span> <span data-ttu-id="bdefd-174">Seleccione **Enable Single Sign On**(Habilitar el inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="bdefd-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="bdefd-175">b.</span><span class="sxs-lookup"><span data-stu-id="bdefd-175">b.</span></span> <span data-ttu-id="bdefd-176">En el cuadro de texto **Identity Provider's Sign-in Page URL** (Dirección URL de la página de inicio de sesión del proveedor de identidades), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bdefd-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bdefd-177">c.</span><span class="sxs-lookup"><span data-stu-id="bdefd-177">c.</span></span> <span data-ttu-id="bdefd-178">En el cuadro de texto **Identity Provider's Sign-out Page URL** (Dirección URL de la página de inicio de sesión del proveedor de identidades, pegue el valor de **URL de cierre de sesión**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bdefd-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bdefd-179">d.</span><span class="sxs-lookup"><span data-stu-id="bdefd-179">d.</span></span> <span data-ttu-id="bdefd-180">Haga clic en **Browse** (Examinar) para cargar el certificado que ha descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bdefd-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="bdefd-181">e.</span><span class="sxs-lookup"><span data-stu-id="bdefd-181">e.</span></span> <span data-ttu-id="bdefd-182">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bdefd-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bdefd-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bdefd-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bdefd-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bdefd-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdefd-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdefd-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdefd-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bdefd-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bdefd-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="bdefd-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bdefd-190">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdefd-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdefd-194">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bdefd-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdefd-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bdefd-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdefd-198">a.</span><span class="sxs-lookup"><span data-stu-id="bdefd-198">a.</span></span> <span data-ttu-id="bdefd-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdefd-200">b.</span><span class="sxs-lookup"><span data-stu-id="bdefd-200">b.</span></span> <span data-ttu-id="bdefd-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdefd-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdefd-202">c.</span><span class="sxs-lookup"><span data-stu-id="bdefd-202">c.</span></span> <span data-ttu-id="bdefd-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bdefd-204">d.</span><span class="sxs-lookup"><span data-stu-id="bdefd-204">d.</span></span> <span data-ttu-id="bdefd-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="bdefd-206">Creación de un usuario de prueba de Origami</span><span class="sxs-lookup"><span data-stu-id="bdefd-206">Creating an Origami test user</span></span>

<span data-ttu-id="bdefd-207">En esta sección, creará un usuario llamado Britta Simon en Origami.</span><span class="sxs-lookup"><span data-stu-id="bdefd-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="bdefd-208">Inicie sesión en la cuenta de Origami con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="bdefd-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="bdefd-209">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="bdefd-211">En el cuadro de diálogo **Users and Security** (Usuarios y seguridad), haga clic en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="bdefd-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="bdefd-213">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="bdefd-213">Click **Add New User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="bdefd-215">En el cuadro de diálogo Add New User (Agregar nuevo usuario), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bdefd-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="bdefd-217">a.</span><span class="sxs-lookup"><span data-stu-id="bdefd-217">a.</span></span> <span data-ttu-id="bdefd-218">En el cuadro de texto **Correo electrónico**, escriba el correo electrónico del usuario, en este caso **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="bdefd-219">b.</span><span class="sxs-lookup"><span data-stu-id="bdefd-219">b.</span></span> <span data-ttu-id="bdefd-220">En el cuadro de texto **Password** (Contraseña), escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="bdefd-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="bdefd-221">c.</span><span class="sxs-lookup"><span data-stu-id="bdefd-221">c.</span></span> <span data-ttu-id="bdefd-222">En el cuadro de texto **Confirm Password** (Confirmar contraseña), escriba la contraseña de nuevo.</span><span class="sxs-lookup"><span data-stu-id="bdefd-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="bdefd-223">d.</span><span class="sxs-lookup"><span data-stu-id="bdefd-223">d.</span></span> <span data-ttu-id="bdefd-224">En el cuadro de texto **First Name** (Nombre), escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="bdefd-225">e.</span><span class="sxs-lookup"><span data-stu-id="bdefd-225">e.</span></span> <span data-ttu-id="bdefd-226">En el cuadro de texto **Last Name** (Apellidos), escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="bdefd-227">f.</span><span class="sxs-lookup"><span data-stu-id="bdefd-227">f.</span></span> <span data-ttu-id="bdefd-228">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-228">Click **Save**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="bdefd-230">Asigne **User Roles** (Roles de usuario) y **Client Access** (Acceso de cliente) al usuario.</span><span class="sxs-lookup"><span data-stu-id="bdefd-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bdefd-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdefd-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bdefd-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Origami.</span><span class="sxs-lookup"><span data-stu-id="bdefd-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bdefd-235">**Para asignar a Britta Simon a Origami, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bdefd-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="bdefd-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bdefd-238">En la lista de aplicaciones, seleccione **Origami**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-238">In the applications list, select **Origami**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="bdefd-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bdefd-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-242">Click **Add** button.</span></span> <span data-ttu-id="bdefd-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bdefd-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bdefd-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bdefd-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdefd-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bdefd-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdefd-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bdefd-248">Testing single sign-on</span></span>

<span data-ttu-id="bdefd-249">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bdefd-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bdefd-250">Al hacer clic en el icono de Origami en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Origami.</span><span class="sxs-lookup"><span data-stu-id="bdefd-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdefd-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bdefd-251">Additional resources</span></span>

* [<span data-ttu-id="bdefd-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdefd-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdefd-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdefd-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

