---
title: "Tutorial: Integración de Azure Active Directory con Abintegro | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Abintegro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="7e012-103">Tutorial: Integración de Azure Active Directory con Abintegro</span><span class="sxs-lookup"><span data-stu-id="7e012-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="7e012-104">En este tutorial, aprenderá a integrar Abintegro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e012-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e012-105">La integración de Abintegro con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7e012-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7e012-106">Puede controlar en Azure AD quién tiene acceso a Abintegro</span><span class="sxs-lookup"><span data-stu-id="7e012-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="7e012-107">Puede permitir que los usuarios inicien sesión automáticamente en Abintegro (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e012-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7e012-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7e012-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e012-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e012-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7e012-110">Prerequisites</span></span>

<span data-ttu-id="7e012-111">Para configurar la integración de Azure AD con Abintegro, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7e012-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="7e012-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e012-113">Una suscripción habilitada para el inicio de sesión único en Abintegro</span><span class="sxs-lookup"><span data-stu-id="7e012-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e012-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7e012-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e012-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7e012-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e012-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7e012-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e012-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e012-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e012-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7e012-118">Scenario description</span></span>
<span data-ttu-id="7e012-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7e012-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e012-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7e012-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e012-121">Incorporación de Abintegro desde la galería</span><span class="sxs-lookup"><span data-stu-id="7e012-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="7e012-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="7e012-123">Incorporación de Abintegro desde la galería</span><span class="sxs-lookup"><span data-stu-id="7e012-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="7e012-124">Para configurar la integración de Abintegro en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7e012-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e012-125">**Para agregar Abintegro desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7e012-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e012-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e012-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e012-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7e012-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7e012-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7e012-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7e012-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e012-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7e012-133">En el cuadro de búsqueda, escriba **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="7e012-133">In the search box, type **Abintegro**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="7e012-135">En el panel de resultados, seleccione **Abintegro** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e012-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e012-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e012-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Abintegro con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e012-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e012-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Abintegro para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e012-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="7e012-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Abintegro.</span><span class="sxs-lookup"><span data-stu-id="7e012-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="7e012-141">Para establecer la relación de vínculo, en Abintegro, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7e012-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7e012-142">Para configurar y probar el inicio de sesión único de Azure AD con Abintegro, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7e012-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e012-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="7e012-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e012-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e012-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e012-145">**[Creación de un usuario de prueba de Abintegro](#creating-an-abintegro-test-user)**: para tener un homólogo de Britta Simon en Abintegro vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e012-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e012-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e012-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e012-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7e012-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e012-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e012-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Abintegro.</span><span class="sxs-lookup"><span data-stu-id="7e012-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="7e012-150">**Para configurar el inicio de sesión único de Azure AD con Abintegro, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7e012-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="7e012-151">En Azure Portal, en la página de integración de la aplicación **Abintegro**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7e012-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7e012-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7e012-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="7e012-155">En la sección **Abintegro Domain and URLs** (Dominio y direcciones URL de Abintegro), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7e012-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="7e012-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`.</span><span class="sxs-lookup"><span data-stu-id="7e012-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7e012-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="7e012-158">This value is not real.</span></span> <span data-ttu-id="7e012-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="7e012-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7e012-160">Póngase en contacto con el [equipo de soporte técnico de Abintegro](mailto:support@abintegro.com) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="7e012-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="7e012-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7e012-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="7e012-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7e012-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e012-165">Para configurar el inicio de sesión único en el lado de **Abintegro**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="7e012-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="7e012-166">Ellos lo configuran para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="7e012-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7e012-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e012-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7e012-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7e012-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7e012-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e012-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e012-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e012-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e012-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7e012-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7e012-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e012-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e012-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e012-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7e012-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e012-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e012-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e012-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7e012-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e012-182">a.</span><span class="sxs-lookup"><span data-stu-id="7e012-182">a.</span></span> <span data-ttu-id="7e012-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e012-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e012-184">b.</span><span class="sxs-lookup"><span data-stu-id="7e012-184">b.</span></span> <span data-ttu-id="7e012-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e012-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e012-186">c.</span><span class="sxs-lookup"><span data-stu-id="7e012-186">c.</span></span> <span data-ttu-id="7e012-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7e012-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7e012-188">d.</span><span class="sxs-lookup"><span data-stu-id="7e012-188">d.</span></span> <span data-ttu-id="7e012-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7e012-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="7e012-190">Creación de un usuario de prueba de Abintegro</span><span class="sxs-lookup"><span data-stu-id="7e012-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="7e012-191">No hay elemento de acción para que configure el aprovisionamiento de usuarios en Abintegro.</span><span class="sxs-lookup"><span data-stu-id="7e012-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="7e012-192">Cuando un usuario asignado intenta iniciar sesión en Abintegro desde el panel de acceso, Abintegro comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="7e012-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="7e012-193">Si no hay cuentas de usuario disponibles, Abintegro crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7e012-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7e012-194">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e012-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7e012-195">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Abintegro.</span><span class="sxs-lookup"><span data-stu-id="7e012-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7e012-197">**Para asignar a Britta Simon a Abintegro, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="7e012-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="7e012-198">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7e012-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7e012-200">En la lista de aplicaciones, seleccione **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="7e012-200">In the applications list, select **Abintegro**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="7e012-202">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e012-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7e012-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7e012-204">Click **Add** button.</span></span> <span data-ttu-id="7e012-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7e012-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7e012-207">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7e012-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7e012-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e012-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e012-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7e012-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e012-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7e012-210">Testing single sign-on</span></span>

<span data-ttu-id="7e012-211">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7e012-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7e012-212">Al hacer clic en el icono de Abintegro del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Abintegro.</span><span class="sxs-lookup"><span data-stu-id="7e012-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="7e012-213">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e012-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e012-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7e012-214">Additional resources</span></span>

* [<span data-ttu-id="7e012-215">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e012-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e012-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e012-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

