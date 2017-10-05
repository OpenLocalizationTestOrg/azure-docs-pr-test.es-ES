---
title: "Tutorial: Integración de Azure Active Directory con Ariba | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="625da-103">Tutorial: Integración de Azure Active Directory con Ariba</span><span class="sxs-lookup"><span data-stu-id="625da-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="625da-104">En este tutorial, obtendrá información sobre cómo integrar Ariba con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="625da-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="625da-105">Integrar Ariba con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="625da-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="625da-106">Puede controlar en Azure AD quién tiene acceso a Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="625da-107">Puede permitir que los usuarios inicien sesión automáticamente en Ariba (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="625da-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="625da-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="625da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="625da-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="625da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="625da-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="625da-110">Prerequisites</span></span>

<span data-ttu-id="625da-111">Para configurar la integración de Azure AD con Ariba, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="625da-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="625da-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="625da-113">Una suscripción habilitada para el inicio de sesión único en Ariba</span><span class="sxs-lookup"><span data-stu-id="625da-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="625da-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="625da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="625da-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="625da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="625da-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="625da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="625da-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="625da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="625da-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="625da-118">Scenario description</span></span>
<span data-ttu-id="625da-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="625da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="625da-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="625da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="625da-121">Incorporación de Ariba desde la galería</span><span class="sxs-lookup"><span data-stu-id="625da-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="625da-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="625da-123">Incorporación de Ariba desde la galería</span><span class="sxs-lookup"><span data-stu-id="625da-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="625da-124">Para configurar la integración de Ariba en Azure AD, es preciso agregar Ariba desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="625da-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="625da-125">**Para agregar Ariba desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="625da-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="625da-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="625da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="625da-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="625da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="625da-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="625da-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="625da-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="625da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="625da-133">En el cuadro de búsqueda, escriba **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="625da-133">In the search box, type **Ariba**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="625da-135">En el panel de resultados, seleccione **Ariba** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="625da-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="625da-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="625da-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Ariba con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="625da-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="625da-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Ariba para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="625da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="625da-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="625da-141">Para establecer la relación de vínculo, en Ariba, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="625da-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="625da-142">Para configurar y probar el inicio de sesión único de Azure AD con Ariba, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="625da-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="625da-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="625da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="625da-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="625da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="625da-145">**[Creación de un usuario de prueba de Ariba](#creating-an-ariba-test-user)**: para tener un homólogo de Britta Simon en Ariba que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="625da-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="625da-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="625da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="625da-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="625da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="625da-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="625da-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="625da-150">**Para configurar el inicio de sesión único de Azure AD con Ariba, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="625da-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="625da-151">En Azure Portal, en la página de integración de la aplicación **Ariba**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="625da-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="625da-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="625da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="625da-155">En la sección **Dominio y direcciones URL de Ariba**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="625da-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="625da-157">a.</span><span class="sxs-lookup"><span data-stu-id="625da-157">a.</span></span> <span data-ttu-id="625da-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.sourcing.ariba.com` o `https://<subdomain>.supplier.ariba.com`.</span><span class="sxs-lookup"><span data-stu-id="625da-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="625da-159">b.</span><span class="sxs-lookup"><span data-stu-id="625da-159">b.</span></span> <span data-ttu-id="625da-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="625da-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="625da-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="625da-161">These values are not real.</span></span> <span data-ttu-id="625da-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="625da-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="625da-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="625da-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="625da-164">Llame al equipo de soporte técnico del cliente de Ariba al **1-866-218-2155** para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="625da-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="625da-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="625da-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="625da-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="625da-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="625da-169">Para configurar el inicio de sesión único para su aplicación, llame al equipo de soporte técnico de Ariba al número de teléfono **1-866-218-2155** y le ayudarán a proporcionarles el archivo **Certificado (Base64)** descargado.</span><span class="sxs-lookup"><span data-stu-id="625da-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="625da-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="625da-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="625da-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="625da-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="625da-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="625da-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="625da-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="625da-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="625da-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="625da-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="625da-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="625da-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="625da-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="625da-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="625da-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="625da-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="625da-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="625da-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="625da-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="625da-185">a.</span><span class="sxs-lookup"><span data-stu-id="625da-185">a.</span></span> <span data-ttu-id="625da-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="625da-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="625da-187">b.</span><span class="sxs-lookup"><span data-stu-id="625da-187">b.</span></span> <span data-ttu-id="625da-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="625da-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="625da-189">c.</span><span class="sxs-lookup"><span data-stu-id="625da-189">c.</span></span> <span data-ttu-id="625da-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="625da-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="625da-191">d.</span><span class="sxs-lookup"><span data-stu-id="625da-191">d.</span></span> <span data-ttu-id="625da-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="625da-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="625da-193">Creación de un usuario de prueba de Ariba</span><span class="sxs-lookup"><span data-stu-id="625da-193">Creating an Ariba test user</span></span>

<span data-ttu-id="625da-194">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="625da-195">Colabore con el equipo de soporte técnico de Ariba en el **1-866-218-2155** para agregar los usuarios en el sistema de Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="625da-196">Si necesita crear manualmente un usuario, es preciso que llame al equipo de soporte técnico de Ariba en el **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="625da-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="625da-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="625da-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="625da-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="625da-200">**Para asignar Britta Simon a Ariba, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="625da-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="625da-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="625da-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="625da-203">En la lista de aplicaciones, seleccione **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="625da-203">In the applications list, select **Ariba**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="625da-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="625da-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="625da-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="625da-207">Click **Add** button.</span></span> <span data-ttu-id="625da-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="625da-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="625da-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="625da-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="625da-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="625da-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="625da-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="625da-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="625da-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="625da-213">Testing single sign-on</span></span>
<span data-ttu-id="625da-214">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="625da-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="625da-215">Al hacer clic en el icono de Ariba en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Ariba.</span><span class="sxs-lookup"><span data-stu-id="625da-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="625da-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="625da-216">Additional resources</span></span>

* [<span data-ttu-id="625da-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="625da-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="625da-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="625da-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

