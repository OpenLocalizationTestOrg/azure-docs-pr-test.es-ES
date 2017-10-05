---
title: "Tutorial: Integración de Azure Active Directory con Jostle | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Jostle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0ca8aca1446a38643ce9f6751b6fe9cae1eaa5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="f9af2-103">Tutorial: Integración de Azure Active Directory con Jostle</span><span class="sxs-lookup"><span data-stu-id="f9af2-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="f9af2-104">En este tutorial, obtendrá información sobre cómo integrar Jostle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9af2-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9af2-105">Integrar Jostle con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f9af2-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9af2-106">Puede controlar en Azure AD quién tiene acceso a Jostle.</span><span class="sxs-lookup"><span data-stu-id="f9af2-106">You can control in Azure AD who has access to Jostle</span></span>
- <span data-ttu-id="f9af2-107">Puede permitir que los usuarios inicien sesión automáticamente en Jostle (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9af2-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9af2-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f9af2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9af2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9af2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9af2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f9af2-110">Prerequisites</span></span>

<span data-ttu-id="f9af2-111">Para configurar la integración de Azure AD con Jostle, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f9af2-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

- <span data-ttu-id="f9af2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9af2-113">Una suscripción habilitada para el inicio de sesión único en Jostle</span><span class="sxs-lookup"><span data-stu-id="f9af2-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9af2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f9af2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9af2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f9af2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9af2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f9af2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9af2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9af2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9af2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f9af2-118">Scenario description</span></span>
<span data-ttu-id="f9af2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f9af2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9af2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f9af2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9af2-121">Adición de Jostle desde la galería</span><span class="sxs-lookup"><span data-stu-id="f9af2-121">Adding Jostle from the gallery</span></span>
2. <span data-ttu-id="f9af2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="f9af2-123">Adición de Jostle desde la galería</span><span class="sxs-lookup"><span data-stu-id="f9af2-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="f9af2-124">Para configurar la integración de Jostle en Azure AD, deberá agregar Jostle desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f9af2-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9af2-125">**Para agregar Jostle desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f9af2-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9af2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9af2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9af2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f9af2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f9af2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f9af2-133">En el cuadro de búsqueda, escriba **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-133">In the search box, type **Jostle**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="f9af2-135">En el panel de resultados, seleccione **Jostle** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9af2-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9af2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9af2-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jostle con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f9af2-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9af2-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Jostle para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9af2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="f9af2-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Jostle.</span><span class="sxs-lookup"><span data-stu-id="f9af2-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="f9af2-141">Para establecer la relación de vínculo, en Jostle, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9af2-142">Para configurar y probar el inicio de sesión único de Azure AD con Jostle, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f9af2-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9af2-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f9af2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9af2-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9af2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9af2-145">**[Creación de un usuario de prueba de Jostle](#creating-a-jostle-test-user)**: para tener un homólogo de Britta Simon en Jostle que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9af2-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9af2-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9af2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9af2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f9af2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9af2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9af2-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Jostle.</span><span class="sxs-lookup"><span data-stu-id="f9af2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="f9af2-150">**Para configurar el inicio de sesión único de Azure AD con Jostle, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f9af2-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="f9af2-151">En Azure Portal, en la página de integración de la aplicación **Jostle**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f9af2-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f9af2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="f9af2-155">En la sección **Dominio y direcciones URL de Jostle**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9af2-155">On the **Jostle Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="f9af2-157">a.</span><span class="sxs-lookup"><span data-stu-id="f9af2-157">a.</span></span> <span data-ttu-id="f9af2-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tanent name>.jostle.us/jostle-prod/`.</span><span class="sxs-lookup"><span data-stu-id="f9af2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="f9af2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9af2-159">b.</span></span> <span data-ttu-id="f9af2-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="f9af2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9af2-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f9af2-161">These values are not real.</span></span> <span data-ttu-id="f9af2-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f9af2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f9af2-163">Póngase en contacto con el [equipo de soporte técnico de Jostle](mailto:support@jostle.me) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="f9af2-163">Contact [Jostle support team](mailto:support@jostle.me) to get these values.</span></span> 
 


4. <span data-ttu-id="f9af2-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f9af2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="f9af2-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f9af2-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f9af2-168">Para configurar el inicio de sesión único en Jostle, necesita enviar el archivo XML de metadatos descargado al [equipo de soporte técnico de Jostle](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="f9af2-168">To configure single sign-on on Jostle side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="f9af2-169">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="f9af2-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="f9af2-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9af2-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9af2-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f9af2-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9af2-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9af2-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9af2-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9af2-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f9af2-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f9af2-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f9af2-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9af2-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9af2-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9af2-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f9af2-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9af2-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f9af2-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9af2-185">a.</span><span class="sxs-lookup"><span data-stu-id="f9af2-185">a.</span></span> <span data-ttu-id="f9af2-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9af2-187">b.</span><span class="sxs-lookup"><span data-stu-id="f9af2-187">b.</span></span> <span data-ttu-id="f9af2-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9af2-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9af2-189">c.</span><span class="sxs-lookup"><span data-stu-id="f9af2-189">c.</span></span> <span data-ttu-id="f9af2-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9af2-191">d.</span><span class="sxs-lookup"><span data-stu-id="f9af2-191">d.</span></span> <span data-ttu-id="f9af2-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="f9af2-193">Creación de un usuario de prueba de Jostle</span><span class="sxs-lookup"><span data-stu-id="f9af2-193">Creating a Jostle test user</span></span>

<span data-ttu-id="f9af2-194">En esta sección, creará un usuario llamado Britta Simon en Jostle.</span><span class="sxs-lookup"><span data-stu-id="f9af2-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="f9af2-195">Si no sabe cómo agregar a Britta Simon en Jostle, póngase en contacto con el [equipo de soporte técnico de Jostle](mailto:support@jostle.me) para agregar al usuario y habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f9af2-195">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="f9af2-196">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="f9af2-196">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9af2-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9af2-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9af2-198">En esta sección, concederá acceso a Britta Simon a Jostle para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9af2-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f9af2-200">**Para asignar a Britta Simon a Jostle, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f9af2-200">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="f9af2-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f9af2-203">En la lista de aplicaciones, seleccione **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-203">In the applications list, select **Jostle**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="f9af2-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f9af2-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-207">Click **Add** button.</span></span> <span data-ttu-id="f9af2-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f9af2-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f9af2-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9af2-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9af2-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f9af2-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9af2-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f9af2-213">Testing single sign-on</span></span>

<span data-ttu-id="f9af2-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f9af2-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f9af2-215">Al hacer clic en el icono de Jostle en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Jostle.</span><span class="sxs-lookup"><span data-stu-id="f9af2-215">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="f9af2-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9af2-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9af2-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f9af2-217">Additional resources</span></span>

* [<span data-ttu-id="f9af2-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9af2-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9af2-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9af2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png
