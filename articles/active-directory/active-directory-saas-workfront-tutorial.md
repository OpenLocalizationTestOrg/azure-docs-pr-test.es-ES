---
title: "Tutorial: integración de Azure Active Directory con Workfront | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="36e15-103">Tutorial: integración de Azure Active Directory con Workfront</span><span class="sxs-lookup"><span data-stu-id="36e15-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="36e15-104">En este tutorial, aprenderá a integrar Workfront con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36e15-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36e15-105">La integración de Workfront con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="36e15-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36e15-106">Puede controlar en Azure AD quién tiene acceso a Workfront</span><span class="sxs-lookup"><span data-stu-id="36e15-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="36e15-107">Puede permitir que los usuarios inicien sesión automáticamente en Workfront (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36e15-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="36e15-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="36e15-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36e15-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36e15-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="36e15-110">Prerequisites</span></span>

<span data-ttu-id="36e15-111">Para configurar la integración de Azure AD con Workfront, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="36e15-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="36e15-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36e15-113">Una suscripción habilitada para el inicio de sesión único en Workfront</span><span class="sxs-lookup"><span data-stu-id="36e15-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36e15-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="36e15-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36e15-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="36e15-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36e15-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="36e15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36e15-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36e15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36e15-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="36e15-118">Scenario description</span></span>
<span data-ttu-id="36e15-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="36e15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36e15-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="36e15-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36e15-121">Adición de Workfront desde la galería</span><span class="sxs-lookup"><span data-stu-id="36e15-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="36e15-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="36e15-123">Adición de Workfront desde la galería</span><span class="sxs-lookup"><span data-stu-id="36e15-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="36e15-124">Para configurar la integración de Workfront en Azure AD, será preciso que agregue Workfront desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="36e15-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36e15-125">**Para agregar Workfront desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="36e15-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36e15-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36e15-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36e15-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="36e15-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36e15-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36e15-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="36e15-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36e15-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="36e15-133">En el cuadro de búsqueda, escriba **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="36e15-133">In the search box, type **Workfront**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="36e15-135">En el panel de resultados, seleccione **Workfront** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36e15-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36e15-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36e15-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Workfront con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36e15-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="36e15-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workfront para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36e15-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="36e15-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workfront.</span><span class="sxs-lookup"><span data-stu-id="36e15-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="36e15-141">En Workfront, para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="36e15-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36e15-142">Para configurar y probar el inicio de sesión único de Azure AD con Workfront, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="36e15-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36e15-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="36e15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36e15-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36e15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36e15-145">**[Creación de un usuario de prueba de Workfront](#creating-a-workfront-test-user)**: para tener un homólogo de Britta Simon en Workfront que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36e15-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="36e15-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36e15-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36e15-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="36e15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36e15-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36e15-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Workfront.</span><span class="sxs-lookup"><span data-stu-id="36e15-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="36e15-150">**Para configurar el inicio de sesión único de Azure AD con Workfront, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="36e15-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="36e15-151">En Azure Portal, en la página de integración de la aplicación **Workfront**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="36e15-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="36e15-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="36e15-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="36e15-155">En la sección **Dominio y direcciones URL de Workfront**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="36e15-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="36e15-157">a.</span><span class="sxs-lookup"><span data-stu-id="36e15-157">a.</span></span> <span data-ttu-id="36e15-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.attask-ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="36e15-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="36e15-159">b.</span><span class="sxs-lookup"><span data-stu-id="36e15-159">b.</span></span> <span data-ttu-id="36e15-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="36e15-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36e15-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="36e15-161">These values are not real.</span></span> <span data-ttu-id="36e15-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="36e15-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36e15-163">Póngase en contacto con el [equipo de soporte de cliente de Workfront](https://www.workfront.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="36e15-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="36e15-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="36e15-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="36e15-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="36e15-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36e15-168">En la sección **Configuración de Workfront**, haga clic en **Configurar Workfront** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="36e15-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36e15-169">Copie los valores de **Dirección URL de cierre de sesión y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="36e15-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="36e15-171">Inicie sesión en su sitio de la empresa Workfront como administrador.</span><span class="sxs-lookup"><span data-stu-id="36e15-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="36e15-172">Vaya a **Single Sign On Configuration**(Configuración de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="36e15-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="36e15-173">En el cuadro de diálogo **Inicio de sesión único** , siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="36e15-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Configurar inicio de sesión único][23]
   
    <span data-ttu-id="36e15-175">a.</span><span class="sxs-lookup"><span data-stu-id="36e15-175">a.</span></span> <span data-ttu-id="36e15-176">En **Tipo**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="36e15-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="36e15-177">b.</span><span class="sxs-lookup"><span data-stu-id="36e15-177">b.</span></span> <span data-ttu-id="36e15-178">Seleccione **Service Provider ID** (Id. del proveedor de servicios).</span><span class="sxs-lookup"><span data-stu-id="36e15-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="36e15-179">c.</span><span class="sxs-lookup"><span data-stu-id="36e15-179">c.</span></span> <span data-ttu-id="36e15-180">En el cuadro de texto **Login Portal URL** (Dirección URL del portal de inicio de sesión), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="36e15-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="36e15-181">d.</span><span class="sxs-lookup"><span data-stu-id="36e15-181">d.</span></span> <span data-ttu-id="36e15-182">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL del servicio de cierre de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="36e15-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="36e15-183">e.</span><span class="sxs-lookup"><span data-stu-id="36e15-183">e.</span></span> <span data-ttu-id="36e15-184">Pegue el valor de **Cambiar dirección URL de contraseña** en el cuadro de texto **Cambiar dirección URL de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="36e15-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="36e15-185">f.</span><span class="sxs-lookup"><span data-stu-id="36e15-185">f.</span></span> <span data-ttu-id="36e15-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="36e15-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="36e15-187">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36e15-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36e15-188">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="36e15-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36e15-189">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36e15-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36e15-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="36e15-191">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36e15-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="36e15-193">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="36e15-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36e15-194">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36e15-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36e15-196">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="36e15-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36e15-198">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36e15-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36e15-200">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="36e15-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36e15-202">a.</span><span class="sxs-lookup"><span data-stu-id="36e15-202">a.</span></span> <span data-ttu-id="36e15-203">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36e15-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36e15-204">b.</span><span class="sxs-lookup"><span data-stu-id="36e15-204">b.</span></span> <span data-ttu-id="36e15-205">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36e15-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36e15-206">c.</span><span class="sxs-lookup"><span data-stu-id="36e15-206">c.</span></span> <span data-ttu-id="36e15-207">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="36e15-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36e15-208">d.</span><span class="sxs-lookup"><span data-stu-id="36e15-208">d.</span></span> <span data-ttu-id="36e15-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="36e15-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="36e15-210">Creación de usuario de prueba de Workfront</span><span class="sxs-lookup"><span data-stu-id="36e15-210">Creating a Workfront test user</span></span>

<span data-ttu-id="36e15-211">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Workfront.</span><span class="sxs-lookup"><span data-stu-id="36e15-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="36e15-212">**Para crear un usuario llamado Britta Simon en Workfront, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="36e15-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="36e15-213">Inicie sesión en su sitio de la empresa Workfront como administrador.</span><span class="sxs-lookup"><span data-stu-id="36e15-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="36e15-214">En el menú de la parte superior, haga clic en **People**(Personas).</span><span class="sxs-lookup"><span data-stu-id="36e15-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="36e15-215">Haga clic en **New Person**(Nueva persona).</span><span class="sxs-lookup"><span data-stu-id="36e15-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="36e15-216">En el cuadro de diálogo Nueva persona, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="36e15-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Crear un usuario de prueba en Workfront][21] 
   
    <span data-ttu-id="36e15-218">a.</span><span class="sxs-lookup"><span data-stu-id="36e15-218">a.</span></span> <span data-ttu-id="36e15-219">En el cuadro de texto **First Name** (Nombre), escriba "Britta".</span><span class="sxs-lookup"><span data-stu-id="36e15-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="36e15-220">b.</span><span class="sxs-lookup"><span data-stu-id="36e15-220">b.</span></span> <span data-ttu-id="36e15-221">En el cuadro de texto **Last Name** (Apellidos), escriba "Simon".</span><span class="sxs-lookup"><span data-stu-id="36e15-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="36e15-222">c.</span><span class="sxs-lookup"><span data-stu-id="36e15-222">c.</span></span> <span data-ttu-id="36e15-223">En el cuadro de texto **E-mail Address** (Dirección de correo electrónico), escriba la dirección de correo electrónico de Britta Simon en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36e15-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="36e15-224">d.</span><span class="sxs-lookup"><span data-stu-id="36e15-224">d.</span></span> <span data-ttu-id="36e15-225">Haga clic en **Add Person**(Agregar persona).</span><span class="sxs-lookup"><span data-stu-id="36e15-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36e15-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36e15-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36e15-227">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Workfront.</span><span class="sxs-lookup"><span data-stu-id="36e15-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="36e15-229">**Para asignar Britta Simon a Workfront, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="36e15-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="36e15-230">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36e15-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="36e15-232">En la lista de aplicaciones, seleccione **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="36e15-232">In the applications list, select **Workfront**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="36e15-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36e15-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="36e15-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="36e15-236">Click **Add** button.</span></span> <span data-ttu-id="36e15-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36e15-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="36e15-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="36e15-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36e15-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36e15-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36e15-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36e15-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36e15-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="36e15-242">Testing single sign-on</span></span>

<span data-ttu-id="36e15-243">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="36e15-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36e15-244">Al hacer clic en el icono de Workfront del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Workfront.</span><span class="sxs-lookup"><span data-stu-id="36e15-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="36e15-245">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36e15-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="36e15-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="36e15-246">Additional resources</span></span>

* [<span data-ttu-id="36e15-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36e15-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36e15-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36e15-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

