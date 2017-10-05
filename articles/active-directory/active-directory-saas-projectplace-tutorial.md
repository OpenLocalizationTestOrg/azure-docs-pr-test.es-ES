---
title: "Tutorial: integración de Azure Active Directory con Projectplace | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="c8798-103">Tutorial: Integración de Azure Active Directory con Projectplace</span><span class="sxs-lookup"><span data-stu-id="c8798-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="c8798-104">En este tutorial aprenderá a integrar Projectplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8798-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8798-105">La integración de Projectplace con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c8798-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c8798-106">Puede controlar en Azure AD quién tiene acceso a Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="c8798-107">Puede permitir que los usuarios inicien sesión automáticamente en Projectplace (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8798-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8798-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8798-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c8798-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8798-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8798-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c8798-110">Prerequisites</span></span>

<span data-ttu-id="c8798-111">Para configurar la integración de Azure AD con Projectplace, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c8798-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="c8798-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8798-113">Una suscripción habilitada para el inicio de sesión único en Projectplace</span><span class="sxs-lookup"><span data-stu-id="c8798-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8798-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c8798-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8798-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c8798-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8798-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c8798-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8798-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8798-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8798-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c8798-118">Scenario description</span></span>
<span data-ttu-id="c8798-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c8798-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8798-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c8798-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8798-121">Adición de Projectplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="c8798-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="c8798-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="c8798-123">Adición de Projectplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="c8798-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="c8798-124">Para configurar la integración de Projectplace en Azure AD, es preciso agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c8798-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c8798-125">**Para agregar Projectplace desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c8798-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c8798-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8798-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8798-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c8798-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c8798-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c8798-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c8798-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8798-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c8798-133">En el cuadro de búsqueda, escriba **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="c8798-133">In the search box, type **Projectplace**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="c8798-135">En el panel de resultados, seleccione **Projectplace** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8798-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8798-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8798-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Projectplace con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c8798-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c8798-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Projectplace para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8798-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="c8798-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="c8798-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c8798-142">Para configurar y probar el inicio de sesión único de Azure AD con Projectplace, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c8798-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c8798-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c8798-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c8798-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8798-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8798-145">**[Creación de un usuario de prueba de Projectplace](#creating-a-projectplace-test-user)**: el objetivo es tener un homólogo de Britta Simon en Projectplace que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8798-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8798-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8798-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8798-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c8798-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8798-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8798-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="c8798-150">**Para configurar el inicio de sesión único de Azure AD con Projectplace, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c8798-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c8798-151">En la página de integración de la aplicación **Projectplace** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c8798-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c8798-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c8798-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="c8798-155">En la sección **Dominio y direcciones URL de Projectplace**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c8798-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="c8798-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company>.projectplace.com`.</span><span class="sxs-lookup"><span data-stu-id="c8798-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8798-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="c8798-158">This value is not real.</span></span> <span data-ttu-id="c8798-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c8798-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c8798-160">Póngase en contacto con el [equipo de atención al cliente de Projectplace](https://success.planview.com/Projectplace/Support) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="c8798-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="c8798-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c8798-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="c8798-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c8798-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c8798-165">Para configurar el inicio de sesión único en **Projectplace**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="c8798-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="c8798-166">Ellos se encargan de realizar esta configuración para que la conexión de SSO de SAML esté establecida correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="c8798-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="c8798-167">La configuración del inicio de sesión único la debe realizar el [equipo de soporte técnico de Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="c8798-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="c8798-168">Tan pronto como se complete la configuración, recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="c8798-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="c8798-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8798-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c8798-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c8798-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c8798-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8798-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8798-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8798-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c8798-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c8798-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c8798-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c8798-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8798-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8798-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c8798-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8798-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8798-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8798-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c8798-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8798-184">a.</span><span class="sxs-lookup"><span data-stu-id="c8798-184">a.</span></span> <span data-ttu-id="c8798-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8798-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8798-186">b.</span><span class="sxs-lookup"><span data-stu-id="c8798-186">b.</span></span> <span data-ttu-id="c8798-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8798-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8798-188">c.</span><span class="sxs-lookup"><span data-stu-id="c8798-188">c.</span></span> <span data-ttu-id="c8798-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c8798-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c8798-190">d.</span><span class="sxs-lookup"><span data-stu-id="c8798-190">d.</span></span> <span data-ttu-id="c8798-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c8798-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="c8798-192">Creación de un usuario de prueba de Projectplace</span><span class="sxs-lookup"><span data-stu-id="c8798-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="c8798-193">Para permitir que los usuarios de Azure AD inicien sesión en Projectplace, deben aprovisionarse en Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="c8798-194">En el caso de Projectplace, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c8798-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="c8798-195">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c8798-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c8798-196">Inicie sesión en el sitio de la compañía **Projectplace** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c8798-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="c8798-197">Vaya a **Personas** y haga clic en **Miembros**.</span><span class="sxs-lookup"><span data-stu-id="c8798-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="c8798-198">![Personas](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="c8798-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="c8798-199">Haga clic en **Agregar miembro**.</span><span class="sxs-lookup"><span data-stu-id="c8798-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="c8798-200">![Agregar miembros](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Agregar miembros")</span><span class="sxs-lookup"><span data-stu-id="c8798-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="c8798-201">En la sección **Agregar miembro** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c8798-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c8798-202">![Nuevos miembros](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Nuevos miembros")</span><span class="sxs-lookup"><span data-stu-id="c8798-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="c8798-203">a.</span><span class="sxs-lookup"><span data-stu-id="c8798-203">a.</span></span> <span data-ttu-id="c8798-204">En el cuadro de texto **Nuevos miembros** , escriba la dirección de correo electrónico de la cuenta de AAD válida que quiera suministrar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="c8798-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="c8798-205">b.</span><span class="sxs-lookup"><span data-stu-id="c8798-205">b.</span></span> <span data-ttu-id="c8798-206">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="c8798-206">Click **Send**.</span></span>

   <span data-ttu-id="c8798-207">Se enviará un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active al titular de la cuenta de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c8798-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="c8798-208">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Projectplace que proporcione Projectplace para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="c8798-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c8798-209">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8798-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c8798-210">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Projectplace.</span><span class="sxs-lookup"><span data-stu-id="c8798-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c8798-212">**Para asignar a Britta Simon a Projectplace, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c8798-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c8798-213">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c8798-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c8798-215">En la lista de aplicaciones, seleccione **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="c8798-215">In the applications list, select **Projectplace**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="c8798-217">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8798-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c8798-219">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c8798-219">Click **Add** button.</span></span> <span data-ttu-id="c8798-220">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c8798-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c8798-222">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c8798-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c8798-223">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8798-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8798-224">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c8798-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8798-225">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c8798-225">Testing single sign-on</span></span>

<span data-ttu-id="c8798-226">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c8798-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c8798-227">Al hacer clic en el icono de Projectplace en el Panel de acceso, debería iniciar sesión automáticamente en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8798-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="c8798-228">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8798-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8798-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c8798-229">Additional resources</span></span>

* [<span data-ttu-id="c8798-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8798-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8798-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8798-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

