---
title: "Tutorial: Integración de Azure Active Directory con BC in the Cloud | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y BC in the Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: ebc95d600eca1027331cd92cfe481d0c3ee833a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="3cb2c-103">Tutorial: Integración de Azure Active Directory con BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="3cb2c-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="3cb2c-104">En este tutorial, aprenderá a integrar BC in the Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cb2c-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cb2c-105">La integración de BC in the Cloud con Azure AD ofrece las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cb2c-106">En Azure AD puede controlar quién tiene acceso a BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="3cb2c-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="3cb2c-107">Puede permitir que los usuarios inicien sesión automáticamente en BC in the Cloud (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cb2c-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3cb2c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cb2c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cb2c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3cb2c-110">Prerequisites</span></span>

<span data-ttu-id="3cb2c-111">Para configurar la integración de Azure AD con BC in the Cloud se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="3cb2c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cb2c-113">Una suscripción habilitada para el inicio de sesión único en BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="3cb2c-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cb2c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cb2c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cb2c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cb2c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cb2c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cb2c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3cb2c-118">Scenario description</span></span>
<span data-ttu-id="3cb2c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cb2c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cb2c-121">Incorporación de BC in the Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="3cb2c-121">Adding BC in the Cloud from the gallery</span></span>
2. <span data-ttu-id="3cb2c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="3cb2c-123">Incorporación de BC in the Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="3cb2c-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="3cb2c-124">Para configurar la integración de BC in the Cloud en Azure AD, necesita agregar BC in the Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cb2c-125">**Para agregar BC in the Cloud desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3cb2c-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cb2c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3cb2c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cb2c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3cb2c-131">Para agregar una aplicación nueva, haga clic en el botón **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3cb2c-133">En el cuadro de búsqueda, escriba **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="3cb2c-135">En el panel de resultados, seleccione **BC in the Cloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cb2c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3cb2c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BC in the Cloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3cb2c-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cb2c-139">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de BC in the Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="3cb2c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="3cb2c-141">Para establecer la relación de vínculo, en BC in the Cloud, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3cb2c-142">Para configurar y probar el inicio de sesión único de Azure AD con BC in the Cloud, es necesario completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cb2c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3cb2c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cb2c-145">**[Creación de un usuario de prueba de BC in the Cloud](#creating-a-bc-in-the-cloud-test-user)**: para tener un homólogo de Britta Simon en BC in the Cloud que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cb2c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cb2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cb2c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cb2c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="3cb2c-150">**Para configurar el inicio de sesión único de Azure AD con BC in the Cloud, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="3cb2c-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3cb2c-151">En la página de integración de la aplicación **BC in the Cloud** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3cb2c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="3cb2c-155">En la sección **Dominio y direcciones URL de BC in the Cloud**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="3cb2c-157">a.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-157">a.</span></span> <span data-ttu-id="3cb2c-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="3cb2c-159">b.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-159">b.</span></span> <span data-ttu-id="3cb2c-160">En el cuadro de texto **Identificador**, escriba una dirección URL como: `https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="3cb2c-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cb2c-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-161">This value is not real.</span></span> <span data-ttu-id="3cb2c-162">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3cb2c-163">Póngase en contacto con el [equipo de soporte técnico del cliente BC in the Cloud](https://www.bcinthecloud.com/supportcenter/) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
4. <span data-ttu-id="3cb2c-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="3cb2c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3cb2c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cb2c-168">Para configurar el inicio de sesión único en **BC in the Cloud**, es preciso enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="3cb2c-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="3cb2c-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3cb2c-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3cb2c-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cb2c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cb2c-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3cb2c-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3cb2c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3cb2c-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3cb2c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cb2c-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cb2c-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cb2c-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cb2c-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3cb2c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cb2c-184">a.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-184">a.</span></span> <span data-ttu-id="3cb2c-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cb2c-186">b.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-186">b.</span></span> <span data-ttu-id="3cb2c-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cb2c-188">c.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-188">c.</span></span> <span data-ttu-id="3cb2c-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3cb2c-190">d.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-190">d.</span></span> <span data-ttu-id="3cb2c-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="3cb2c-192">Creación de un usuario de prueba de BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="3cb2c-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="3cb2c-193">En esta sección, creará el usuario Britta Simon en BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="3cb2c-194">Trabaje en conjunto con el [equipo de soporte técnico del cliente BC in the Cloud](https://www.bcinthecloud.com/supportcenter/) para agregar los usuarios en la aplicación BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="3cb2c-195">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3cb2c-196">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cb2c-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3cb2c-197">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3cb2c-199">**Para asignar Britta Simon a BC in the Cloud, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3cb2c-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3cb2c-200">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3cb2c-202">En la lista de aplicaciones, seleccione **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="3cb2c-204">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3cb2c-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-206">Click **Add** button.</span></span> <span data-ttu-id="3cb2c-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3cb2c-209">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3cb2c-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cb2c-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cb2c-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3cb2c-212">Testing single sign-on</span></span>

<span data-ttu-id="3cb2c-213">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="3cb2c-214">Al hacer clic en el icono de BC in the Cloud en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="3cb2c-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="3cb2c-215">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cb2c-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cb2c-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3cb2c-216">Additional resources</span></span>

* [<span data-ttu-id="3cb2c-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cb2c-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cb2c-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cb2c-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

