---
title: "Tutorial: integración de Azure Active Directory con 15Five | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="9c549-103">Tutorial: integración de Azure Active Directory con 15Five</span><span class="sxs-lookup"><span data-stu-id="9c549-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="9c549-104">En este tutorial, obtendrá información sobre cómo integrar 15Five con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c549-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c549-105">Integrar 15Five con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9c549-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9c549-106">Puede controlar en Azure AD quién tiene acceso a 15Five</span><span class="sxs-lookup"><span data-stu-id="9c549-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="9c549-107">Puede permitir que los usuarios inicien sesión automáticamente en 15Five (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9c549-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9c549-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9c549-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c549-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c549-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9c549-110">Prerequisites</span></span>

<span data-ttu-id="9c549-111">Para configurar la integración de Azure AD con 15Five, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9c549-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="9c549-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c549-113">Una suscripción habilitada para el inicio de sesión único en 15Five</span><span class="sxs-lookup"><span data-stu-id="9c549-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c549-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9c549-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c549-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9c549-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c549-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9c549-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c549-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c549-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c549-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9c549-118">Scenario description</span></span>
<span data-ttu-id="9c549-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9c549-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c549-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9c549-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c549-121">Adición de 15Five desde la galería</span><span class="sxs-lookup"><span data-stu-id="9c549-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="9c549-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="9c549-123">Adición de 15Five desde la galería</span><span class="sxs-lookup"><span data-stu-id="9c549-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="9c549-124">Para configurar la integración de 15Five en Azure AD, tendrá que agregar 15Five desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9c549-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9c549-125">**Para agregar 15Five desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9c549-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9c549-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c549-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9c549-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9c549-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9c549-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9c549-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9c549-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9c549-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9c549-133">En el cuadro de búsqueda, escriba **15Five**.</span><span class="sxs-lookup"><span data-stu-id="9c549-133">In the search box, type **15Five**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="9c549-135">En el panel de resultados, seleccione **15Five** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c549-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9c549-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9c549-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 15Five con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9c549-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9c549-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de 15Five para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c549-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="9c549-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de 15Five.</span><span class="sxs-lookup"><span data-stu-id="9c549-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="9c549-141">Para establecer la relación de vínculo, en 15Five, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9c549-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9c549-142">Para configurar y probar el inicio de sesión único de Azure AD con 15Five, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9c549-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9c549-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9c549-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9c549-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c549-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c549-145">**[Creación de un usuario de prueba de 15Five](#creating-a-15five-test-user)**: para tener un homólogo de Britta Simon en 15Five que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="9c549-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c549-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c549-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c549-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9c549-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9c549-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9c549-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación 15Five.</span><span class="sxs-lookup"><span data-stu-id="9c549-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="9c549-150">**Para configurar el inicio de sesión único de Azure AD con 15Five, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9c549-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="9c549-151">En Azure Portal, en la página de integración de la aplicación **15Five**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9c549-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9c549-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9c549-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="9c549-155">En la sección **Dominio y direcciones URL de 15Five**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9c549-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="9c549-157">a.</span><span class="sxs-lookup"><span data-stu-id="9c549-157">a.</span></span> <span data-ttu-id="9c549-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.15five.com`.</span><span class="sxs-lookup"><span data-stu-id="9c549-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="9c549-159">b.</span><span class="sxs-lookup"><span data-stu-id="9c549-159">b.</span></span> <span data-ttu-id="9c549-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="9c549-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c549-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9c549-161">These values are not real.</span></span> <span data-ttu-id="9c549-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9c549-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9c549-163">Póngase en contacto con el [equipo de soporte de cliente de 15Five](https://www.15five.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9c549-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="9c549-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9c549-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="9c549-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9c549-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9c549-168">Para configurar el inicio de sesión único en el lado de **15Five**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="9c549-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="9c549-169">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c549-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9c549-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9c549-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9c549-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c549-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9c549-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9c549-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9c549-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9c549-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9c549-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9c549-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c549-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9c549-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9c549-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9c549-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9c549-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9c549-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9c549-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9c549-184">a.</span><span class="sxs-lookup"><span data-stu-id="9c549-184">a.</span></span> <span data-ttu-id="9c549-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c549-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c549-186">b.</span><span class="sxs-lookup"><span data-stu-id="9c549-186">b.</span></span> <span data-ttu-id="9c549-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c549-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9c549-188">c.</span><span class="sxs-lookup"><span data-stu-id="9c549-188">c.</span></span> <span data-ttu-id="9c549-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9c549-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9c549-190">d.</span><span class="sxs-lookup"><span data-stu-id="9c549-190">d.</span></span> <span data-ttu-id="9c549-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9c549-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="9c549-192">Creación de un usuario de prueba de 15Five</span><span class="sxs-lookup"><span data-stu-id="9c549-192">Creating a 15Five test user</span></span>

<span data-ttu-id="9c549-193">Para permitir que los usuarios de Azure AD inicien sesión en 15Five, es necesario que se aprovisionen en 15Five.</span><span class="sxs-lookup"><span data-stu-id="9c549-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="9c549-194">En el caso de 15Five, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9c549-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="9c549-195">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="9c549-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="9c549-196">Inicie sesión en el sitio de la compañía de **15Five** como administrador.</span><span class="sxs-lookup"><span data-stu-id="9c549-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="9c549-197">Vaya a **Administrar compañía**.</span><span class="sxs-lookup"><span data-stu-id="9c549-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="9c549-198">![Administrar compañía](./media/active-directory-saas-15five-tutorial/IC784675.png "Administrar compañía")</span><span class="sxs-lookup"><span data-stu-id="9c549-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="9c549-199">Vaya a **Contactos \> Agregar contactos**.</span><span class="sxs-lookup"><span data-stu-id="9c549-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="9c549-200">![Personas](./media/active-directory-saas-15five-tutorial/IC784676.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="9c549-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="9c549-201">En la sección Add New Person (Agregar nueva persona), lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9c549-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="9c549-202">![Agregar nueva persona](./media/active-directory-saas-15five-tutorial/IC784677.png "Agregar nueva persona")</span><span class="sxs-lookup"><span data-stu-id="9c549-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="9c549-203">a.</span><span class="sxs-lookup"><span data-stu-id="9c549-203">a.</span></span> <span data-ttu-id="9c549-204">Especifique **First Name** (Nombre), **Last Name** (Apellido), **Title** (Título), **Email address** (dirección de correo electrónico) de una cuenta de Azure Active Directory válida que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="9c549-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="9c549-205">b.</span><span class="sxs-lookup"><span data-stu-id="9c549-205">b.</span></span> <span data-ttu-id="9c549-206">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="9c549-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="9c549-207">El titular de la cuenta de Azure AD recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="9c549-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9c549-208">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c549-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9c549-209">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a 15Five.</span><span class="sxs-lookup"><span data-stu-id="9c549-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9c549-211">**Para asignar a Britta Simon a 15Five, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9c549-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="9c549-212">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9c549-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9c549-214">En la lista de aplicaciones, seleccione **15Five**.</span><span class="sxs-lookup"><span data-stu-id="9c549-214">In the applications list, select **15Five**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="9c549-216">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9c549-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9c549-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9c549-218">Click **Add** button.</span></span> <span data-ttu-id="9c549-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9c549-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9c549-221">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9c549-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9c549-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9c549-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c549-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9c549-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9c549-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9c549-224">Testing single sign-on</span></span>

<span data-ttu-id="9c549-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9c549-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9c549-226">Al hacer clic en el icono de 15Five del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación 15Five.</span><span class="sxs-lookup"><span data-stu-id="9c549-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="9c549-227">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c549-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9c549-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9c549-228">Additional resources</span></span>

* [<span data-ttu-id="9c549-229">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c549-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c549-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c549-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

