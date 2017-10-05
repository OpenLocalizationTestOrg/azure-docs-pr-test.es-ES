---
title: "Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Splunk Enterprise y Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 181d0f33245f0811c15c1e7945c797502ef71eba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="be928-103">Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="be928-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="be928-104">En este tutorial, aprenderá a integrar Splunk Enterprise y Splunk Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be928-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be928-105">La integración de Splunk Enterprise y Splunk Cloud con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="be928-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be928-106">Puede controlar en Azure AD quién tiene acceso a Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="be928-107">Puede permitir que los usuarios inicien sesión automáticamente en Splunk Enterprise y Splunk Cloud (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be928-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be928-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="be928-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be928-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be928-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be928-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="be928-110">Prerequisites</span></span>

<span data-ttu-id="be928-111">Para configurar la integración de Azure AD con Splunk Enterprise y Splunk Cloud, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="be928-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="be928-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be928-113">Una suscripción habilitada para inicio de sesión único en Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="be928-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be928-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="be928-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be928-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="be928-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be928-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="be928-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be928-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be928-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be928-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="be928-118">Scenario description</span></span>
<span data-ttu-id="be928-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="be928-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be928-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="be928-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be928-121">Adición de Splunk Enterprise y Splunk Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="be928-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="be928-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="be928-123">Adición de Splunk Enterprise y Splunk Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="be928-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="be928-124">Para configurar la integración de Splunk Enterprise y Splunk Cloud en Azure AD, deberá agregar Splunk Enterprise y Splunk Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="be928-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be928-125">**Para agregar Splunk Enterprise y Splunk Cloud desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="be928-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be928-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be928-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be928-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="be928-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be928-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="be928-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="be928-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be928-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="be928-133">En el cuadro de búsqueda, escriba **Splunk Enterprise y Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="be928-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="be928-135">En el panel de resultados, seleccione **Splunk Enterprise y Splunk Cloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be928-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be928-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be928-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud mediante un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be928-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be928-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Splunk Enterprise y Splunk Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be928-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="be928-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="be928-141">En Splunk Enterprise y Splunk Cloud, esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="be928-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be928-142">Para configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="be928-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be928-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="be928-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be928-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be928-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be928-145">**[Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**: para tener un homólogo de Britta Simon en Splunk Enterprise y Splunk Cloud que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be928-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be928-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be928-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be928-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="be928-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be928-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be928-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="be928-150">**Para configurar el inicio de sesión único en Azure AD con Splunk Enterprise y Splunk Cloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="be928-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="be928-151">En Azure Portal, en la página de integración de la aplicación **Splunk Enterprise y Splunk Cloud**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="be928-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="be928-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="be928-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="be928-155">En la sección **Splunk Enterprise and Splunk Cloud Domain and URLs** (Dominio y direcciones URL de Splunk Enterprise y Splunk Cloud), si quiere configurar la aplicación en el modo iniciado por **IdP**:</span><span class="sxs-lookup"><span data-stu-id="be928-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="be928-157">a.</span><span class="sxs-lookup"><span data-stu-id="be928-157">a.</span></span> <span data-ttu-id="be928-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<splunkserverUrl>/en-US/app/launcher/home`.</span><span class="sxs-lookup"><span data-stu-id="be928-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="be928-159">b.</span><span class="sxs-lookup"><span data-stu-id="be928-159">b.</span></span> <span data-ttu-id="be928-160">En el cuadro de texto **Identificador**, escriba la dirección URL de su instancia de Splunk Server:</span><span class="sxs-lookup"><span data-stu-id="be928-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>

    <span data-ttu-id="be928-161">c.</span><span class="sxs-lookup"><span data-stu-id="be928-161">c.</span></span> <span data-ttu-id="be928-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<splunkserver>/saml/acs`.</span><span class="sxs-lookup"><span data-stu-id="be928-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be928-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="be928-163">These values are not real.</span></span> <span data-ttu-id="be928-164">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="be928-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="be928-165">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="be928-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="be928-166">Póngase en contacto con el [equipo de soporte de cliente de Splunk Enterprise y Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="be928-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span></span> 

4. <span data-ttu-id="be928-167">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="be928-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="be928-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="be928-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be928-171">Para configurar el inicio de sesión único en el lado de **Splunk Enterprise y Splunk Cloud**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Splunk Enterprise y Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="be928-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="be928-172">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be928-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be928-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="be928-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be928-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be928-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be928-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="be928-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="be928-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="be928-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="be928-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be928-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be928-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be928-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="be928-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be928-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be928-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be928-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="be928-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be928-187">a.</span><span class="sxs-lookup"><span data-stu-id="be928-187">a.</span></span> <span data-ttu-id="be928-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be928-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be928-189">b.</span><span class="sxs-lookup"><span data-stu-id="be928-189">b.</span></span> <span data-ttu-id="be928-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be928-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be928-191">c.</span><span class="sxs-lookup"><span data-stu-id="be928-191">c.</span></span> <span data-ttu-id="be928-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="be928-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="be928-193">d.</span><span class="sxs-lookup"><span data-stu-id="be928-193">d.</span></span> <span data-ttu-id="be928-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="be928-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="be928-195">Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="be928-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="be928-196">En esta sección, creará un usuario llamado Britta Simon en Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="be928-197">Trabaje con el [equipo de soporte técnico de Splunk Enterprise y Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) para agregar los usuarios a la plataforma de Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="be928-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="be928-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="be928-199">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="be928-201">**Para asignar Britta Simon a Splunk Enterprise y Splunk Cloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="be928-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="be928-202">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="be928-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="be928-204">En la lista de aplicaciones, seleccione **Splunk Enterprise y Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="be928-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="be928-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="be928-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="be928-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="be928-208">Click **Add** button.</span></span> <span data-ttu-id="be928-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="be928-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="be928-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="be928-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be928-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="be928-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be928-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="be928-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be928-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="be928-214">Testing single sign-on</span></span>

<span data-ttu-id="be928-215">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="be928-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="be928-216">Al hacer clic en el icono de Splunk Enterprise y Splunk Cloud en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="be928-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be928-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="be928-217">Additional resources</span></span>

* [<span data-ttu-id="be928-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be928-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be928-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="be928-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

