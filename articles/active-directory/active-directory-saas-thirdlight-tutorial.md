---
title: "Tutorial: integración de Azure Active Directory con ThirdLight | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="2194f-103">Tutorial: integración de Azure Active Directory con ThirdLight</span><span class="sxs-lookup"><span data-stu-id="2194f-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="2194f-104">En este tutorial, aprenderá a integrar ThirdLight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2194f-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2194f-105">La integración de ThirdLight con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2194f-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2194f-106">En Azure AD se puede controlar quién tiene acceso a ThirdLight</span><span class="sxs-lookup"><span data-stu-id="2194f-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="2194f-107">Puede permitir que los usuarios inicien sesión automáticamente en ThirdLight (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2194f-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2194f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2194f-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2194f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2194f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2194f-110">Prerequisites</span></span>

<span data-ttu-id="2194f-111">Para configurar la integración de Azure AD con ThirdLight, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2194f-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="2194f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2194f-113">Una suscripción habilitada para el inicio de sesión único en ThirdLight</span><span class="sxs-lookup"><span data-stu-id="2194f-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2194f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2194f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2194f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2194f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2194f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2194f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2194f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2194f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2194f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2194f-118">Scenario description</span></span>
<span data-ttu-id="2194f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2194f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2194f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2194f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2194f-121">Incorporación de ThirdLight desde la galería</span><span class="sxs-lookup"><span data-stu-id="2194f-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="2194f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="2194f-123">Incorporación de ThirdLight desde la galería</span><span class="sxs-lookup"><span data-stu-id="2194f-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="2194f-124">Para configurar la integración de ThirdLight en Azure AD, es preciso agregar ThirdLight desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2194f-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2194f-125">**Para agregar ThirdLight desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2194f-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2194f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2194f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2194f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2194f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2194f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2194f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2194f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2194f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2194f-133">En el cuadro de búsqueda, escriba **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="2194f-133">In the search box, type **ThirdLight**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="2194f-135">En el panel de resultados, seleccione **ThirdLight** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2194f-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2194f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2194f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ThirdLight con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2194f-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2194f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ThirdLight para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2194f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="2194f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="2194f-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como valor de **Nombre de usuario** en ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="2194f-142">Para configurar y probar el inicio de sesión único de Azure AD con ThirdLight, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2194f-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2194f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2194f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2194f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2194f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2194f-145">**[Creación de un usuario de prueba de ThirdLight](#creating-a-thirdlight-test-user)**: para tener un homólogo de Britta Simon en ThirdLight vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2194f-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2194f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2194f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2194f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2194f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2194f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2194f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="2194f-150">**Para configurar el inicio de sesión único de Azure AD con ThirdLight, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2194f-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="2194f-151">En Azure Portal, en la página de integración de la aplicación **ThirdLight**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2194f-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2194f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2194f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="2194f-155">En la sección de **ThirdLight Domain and URLs** (Dominio y direcciones URL de ThirdLight), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2194f-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="2194f-157">a.</span><span class="sxs-lookup"><span data-stu-id="2194f-157">a.</span></span> <span data-ttu-id="2194f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.thirdlight.com/`.</span><span class="sxs-lookup"><span data-stu-id="2194f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="2194f-159">b.</span><span class="sxs-lookup"><span data-stu-id="2194f-159">b.</span></span> <span data-ttu-id="2194f-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="2194f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2194f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2194f-161">These values are not real.</span></span> <span data-ttu-id="2194f-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2194f-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="2194f-163">Póngase en contacto con el [equipo de soporte de cliente de ThirdLight](https://www.thirdlight.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="2194f-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="2194f-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2194f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="2194f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2194f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2194f-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de ThirdLight como administrador.</span><span class="sxs-lookup"><span data-stu-id="2194f-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="2194f-169">Vaya a **Configuración \> Administración del sistema** y luego haga clic en **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="2194f-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="2194f-170">![Administración del sistema](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administración del sistema")</span><span class="sxs-lookup"><span data-stu-id="2194f-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="2194f-171">En la sección de configuración de SAML2, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2194f-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="2194f-172">![Inicio de sesión único SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="2194f-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="2194f-173">a.</span><span class="sxs-lookup"><span data-stu-id="2194f-173">a.</span></span> <span data-ttu-id="2194f-174">Seleccione **Habilitar inicio de sesión único de SAML2**.</span><span class="sxs-lookup"><span data-stu-id="2194f-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="2194f-175">b.</span><span class="sxs-lookup"><span data-stu-id="2194f-175">b.</span></span> <span data-ttu-id="2194f-176">Como **Origen para los metadatos de IdP**, seleccione **Cargar metadatos de IdP desde XML**.</span><span class="sxs-lookup"><span data-stu-id="2194f-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="2194f-177">c.</span><span class="sxs-lookup"><span data-stu-id="2194f-177">c.</span></span> <span data-ttu-id="2194f-178">Abra el archivo de metadatos descargado, copie el contenido y luego péguelo en el cuadro de texto **XML de metadatos de IdP** .</span><span class="sxs-lookup"><span data-stu-id="2194f-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="2194f-179">d.</span><span class="sxs-lookup"><span data-stu-id="2194f-179">d.</span></span> <span data-ttu-id="2194f-180">Haga clic en **Guardar configuración de SAML2**.</span><span class="sxs-lookup"><span data-stu-id="2194f-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2194f-181">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2194f-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2194f-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2194f-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2194f-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2194f-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2194f-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="2194f-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2194f-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2194f-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2194f-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2194f-188">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2194f-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2194f-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2194f-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2194f-192">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2194f-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2194f-194">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2194f-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2194f-196">a.</span><span class="sxs-lookup"><span data-stu-id="2194f-196">a.</span></span> <span data-ttu-id="2194f-197">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2194f-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2194f-198">b.</span><span class="sxs-lookup"><span data-stu-id="2194f-198">b.</span></span> <span data-ttu-id="2194f-199">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2194f-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="2194f-200">c.</span><span class="sxs-lookup"><span data-stu-id="2194f-200">c.</span></span> <span data-ttu-id="2194f-201">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2194f-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2194f-202">d.</span><span class="sxs-lookup"><span data-stu-id="2194f-202">d.</span></span> <span data-ttu-id="2194f-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2194f-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="2194f-204">Creación de un usuario de prueba ThirdLight</span><span class="sxs-lookup"><span data-stu-id="2194f-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="2194f-205">Para permitir que los usuarios de Azure AD inicien sesión en ThirdLight, deben aprovisionarse en ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="2194f-206">En el caso de ThirdLight, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2194f-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="2194f-207">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2194f-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2194f-208">Inicie sesión en su sitio de la compañía de **ThirdLight** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2194f-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="2194f-209">Vaya a la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="2194f-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="2194f-210">Seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2194f-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="2194f-211">Haga clic en el botón **Agregar nuevo usuario** .</span><span class="sxs-lookup"><span data-stu-id="2194f-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="2194f-212">Escriba **el nombre de usuario, el nombre o la descripción, el correo electrónico, elegir un valor preestablecido o grupo de nuevos miembros** de una cuenta de AAD válida que quiera suministrar.</span><span class="sxs-lookup"><span data-stu-id="2194f-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="2194f-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2194f-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="2194f-214">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Thirdlight ofrecida por Thirdlight para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="2194f-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2194f-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2194f-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2194f-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2194f-218">**Para asignar Britta Simon a ThirdLight, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2194f-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="2194f-219">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2194f-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2194f-221">En la lista de aplicaciones, seleccione **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="2194f-221">In the applications list, select **ThirdLight**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="2194f-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2194f-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2194f-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2194f-225">Click **Add** button.</span></span> <span data-ttu-id="2194f-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2194f-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2194f-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2194f-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2194f-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2194f-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2194f-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2194f-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2194f-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2194f-231">Testing single sign-on</span></span>

<span data-ttu-id="2194f-232">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2194f-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2194f-233">Al hacer clic en el icono de ThirdLight en el panel de acceso, iniciará sesión automáticamente en la aplicación ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="2194f-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="2194f-234">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2194f-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2194f-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2194f-235">Additional resources</span></span>

* [<span data-ttu-id="2194f-236">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2194f-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2194f-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2194f-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

