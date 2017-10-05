---
title: "Tutorial: Integración de Azure Active Directory con Skillport | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="52eee-103">Tutorial: Integración de Azure Active Directory con Skillport</span><span class="sxs-lookup"><span data-stu-id="52eee-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="52eee-104">En este tutorial, aprenderá a integrar Skillport con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52eee-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52eee-105">La integración de Skillport con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="52eee-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52eee-106">Puede controlar en Azure AD quién tiene acceso a Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="52eee-107">Puede permitir que los usuarios inicien sesión automáticamente en Skillport (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eee-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52eee-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="52eee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52eee-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52eee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52eee-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52eee-110">Prerequisites</span></span>

<span data-ttu-id="52eee-111">Para configurar la integración de Azure AD con Skillport, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="52eee-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="52eee-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52eee-113">Una suscripción habilitada para el inicio de sesión único en Skillport</span><span class="sxs-lookup"><span data-stu-id="52eee-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52eee-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="52eee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52eee-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="52eee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52eee-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="52eee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52eee-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52eee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52eee-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="52eee-118">Scenario description</span></span>
<span data-ttu-id="52eee-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="52eee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52eee-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="52eee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52eee-121">Adición de Skillport desde la galería</span><span class="sxs-lookup"><span data-stu-id="52eee-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="52eee-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="52eee-123">Adición de Skillport desde la galería</span><span class="sxs-lookup"><span data-stu-id="52eee-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="52eee-124">Para configurar la integración de Skillport en Azure AD, es preciso agregar Skillport desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="52eee-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52eee-125">**Para agregar Skillport desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52eee-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52eee-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52eee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52eee-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="52eee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52eee-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52eee-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="52eee-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52eee-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="52eee-133">En el cuadro de búsqueda, escriba **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="52eee-133">In the search box, type **Skillport**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="52eee-135">En el panel de resultados, seleccione **Skillport** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52eee-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52eee-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52eee-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Skillport con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52eee-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52eee-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Skillport para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="52eee-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="52eee-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="52eee-142">Para configurar y probar el inicio de sesión único de Azure AD con Skillport, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="52eee-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52eee-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="52eee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52eee-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52eee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52eee-145">**[Creación de un usuario de prueba de Skillport](#creating-a-skillport-test-user)**: el objetivo es tener un homólogo de Britta Simon en Skillport que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eee-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52eee-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52eee-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="52eee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52eee-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52eee-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="52eee-150">**Para configurar el inicio de sesión único de Azure AD con Skillport, siga los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52eee-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="52eee-151">En la página de integración de la aplicación **Skillport** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="52eee-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="52eee-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52eee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="52eee-155">En la sección **Dominio y direcciones URL de Skillport**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="52eee-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="52eee-157">a.</span><span class="sxs-lookup"><span data-stu-id="52eee-157">a.</span></span> <span data-ttu-id="52eee-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="52eee-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="52eee-159">Centro de datos de UE: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="52eee-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="52eee-160">Centro de datos de EE. UU.: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="52eee-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="52eee-161">b.</span><span class="sxs-lookup"><span data-stu-id="52eee-161">b.</span></span> <span data-ttu-id="52eee-162">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="52eee-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="52eee-163">Centro de datos de UE: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="52eee-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="52eee-164">Centro de datos de EE. UU.: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="52eee-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52eee-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="52eee-165">These values are not the real.</span></span> <span data-ttu-id="52eee-166">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="52eee-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="52eee-167">Póngase en contacto con el [equipo de soporte de cliente de Skillport](https://www.skillsoft.com/contact.asp) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="52eee-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="52eee-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52eee-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="52eee-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="52eee-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52eee-172">Para configurar el inicio de sesión único en **Skillport**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="52eee-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="52eee-173">Ellos se encargarán de configurarlo para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="52eee-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52eee-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="52eee-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52eee-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="52eee-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="52eee-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52eee-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52eee-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52eee-180">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="52eee-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52eee-182">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="52eee-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52eee-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="52eee-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52eee-186">a.</span><span class="sxs-lookup"><span data-stu-id="52eee-186">a.</span></span> <span data-ttu-id="52eee-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52eee-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52eee-188">b.</span><span class="sxs-lookup"><span data-stu-id="52eee-188">b.</span></span> <span data-ttu-id="52eee-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52eee-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52eee-190">c.</span><span class="sxs-lookup"><span data-stu-id="52eee-190">c.</span></span> <span data-ttu-id="52eee-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="52eee-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52eee-192">d.</span><span class="sxs-lookup"><span data-stu-id="52eee-192">d.</span></span> <span data-ttu-id="52eee-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="52eee-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="52eee-194">Creación de un usuario de prueba de Skillport</span><span class="sxs-lookup"><span data-stu-id="52eee-194">Creating a Skillport test user</span></span>

<span data-ttu-id="52eee-195">Para crear el usuario de prueba de Skillport, debe ponerse en contacto con el [equipo de soporte técnico de Skillport](https://www.skillsoft.com/contact.asp) ya que disponen de varios escenarios empresariales acordes con los requisitos del usuario final.</span><span class="sxs-lookup"><span data-stu-id="52eee-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="52eee-196">Después de mantener conversaciones con los usuarios, procederán a configurarlo.</span><span class="sxs-lookup"><span data-stu-id="52eee-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52eee-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eee-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52eee-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="52eee-200">**Para asignar a Britta Simon a Skillport, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="52eee-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="52eee-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52eee-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="52eee-203">En la lista de aplicaciones, seleccione **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="52eee-203">In the applications list, select **Skillport**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="52eee-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52eee-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="52eee-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="52eee-207">Click **Add** button.</span></span> <span data-ttu-id="52eee-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52eee-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="52eee-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="52eee-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52eee-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52eee-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52eee-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52eee-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52eee-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="52eee-213">Testing single sign-on</span></span>

<span data-ttu-id="52eee-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="52eee-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52eee-215">Al hacer clic en el icono de Skillport en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Skillport.</span><span class="sxs-lookup"><span data-stu-id="52eee-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="52eee-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="52eee-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52eee-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="52eee-217">Additional resources</span></span>

* [<span data-ttu-id="52eee-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52eee-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52eee-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52eee-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

